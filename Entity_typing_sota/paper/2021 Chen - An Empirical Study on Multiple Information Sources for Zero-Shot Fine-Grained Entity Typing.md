https://aclanthology.org/2021.emnlp-main.210.pdf

Abstract
---

Auxiliary information from multiple sources has been demonstrated to be effective in [[Zero Shot Fine Grained Entity Typing|zero shot fine-grained entity typing (ZFET)]]. However, there lacks a comprehensive understanding about how to make better use of the existing information sources and how they affect the performance of ZFET. In this paper, we empirically study three kinds of auxiliary information: context consistency, type hierarchy and background knowledge (e.g., prototypes and descriptions) of types, and propose a multi-source fusion model (MSF) targeting these sources. 

![[2021_chen_architecture.png]]

## Introduction
The major challenge of ZFET is to build the semantic connections between the seen types (during training) and the unseen ones (during inference). Auxiliary information has been proved to be essential in this regard (Xian et al., 2019), with a variety of approaches focused on scattered information (Ma et al., 2016; Zhou et al., 2018; Obeidat et al., 2019; Ren et al., 2020; Zhang et al., 2020b).
However, the power of auxiliary information has not been sufficiently exploited in existing solutions. Besides, the effects of each information source also remain to be clearly understood.

In this paper, we propose a Multi-Source Fusion model (MSF) integrating three kinds of popular auxiliary information for ZFET, i.e., context consistency, type hierarchy, and background knowledge, as illustrated in Figure 1.

- Context consistency means a correct type should be semantically consistent with the context if we replace the mention with the type name in the context. Type name is the surface form of a type, which is a word or a phase, e.g., type name of /organization/corporation is corporation.
- Type hierarchy is the ontology structure connecting seen and unseen types
- Background knowledge provides the external prior information that depicts types in detail, e.g., prototypes [[2016 Ma - Label Embedding for Zero-shot Fine-grained Named Entity Typing|(Ma et al., 2016)]] and descriptions [[2019 Obeidat - Description-Based Zero-shot Fine-Grained Entity Typing|(Obeidat et al., 2019)]]. 


MSF is composed of three modules, with each targeting a specific information source. 
	- In the CA (Context-Consistency Aware) module, we measure the context consistency by large-scale pretrained language models, e.g., BERT (Devlin et al., 2019). By masking mentions and predicting the names of ground truth types through finetuning on the data of seen types, CA is expected to measure the context consistency of unseen types more precisely. 
	- In the HA (Type-Hierarchy Aware) module, we use Transformer encoder (Vaswani et al., 2017) to model the hierarchical dependency among types. There have been substantial works exploring type hierarchy in the supervised typing task (Shimaoka et al., 2017; Xu and Barbosa, 2018; Xiong et al., 2019), but only some preliminary research in ZFET (Ma et al., 2016; Zhang et al., 2020b). 
	- In the KA (Background-Knowledge Aware) module, we introduce prototypes (Ma et al., 2016) and WordNet descriptions (Miller, 1995) as background knowledge of types. KA is embodied as natural language inference with a translation-based solution to better incorporate knowledge

In summary, our contributions are as follows:  
	- We propose a multi-source fusion model integrating multiple information sources for ZFET, which achieves new state-of-the-art results on BBN and Wiki
	- We are the first work to conduct a comprehensive study on the strengths and weaknesses of three auxiliary information sources for ZFET. Besides, we also make a deep analysis about how different information sources complement each other and how they contribute to the proposed fusion model.

## Model Architecture
#### Context-Consistency-Aware (CA) Module 
We base the CA module upon the pre-trained BERT (Devlin et al., 2019) and fine-tune it for assessment of context consistency

**Fine Tuning**

tl:dr - they mask the entity mention and ask the BERT to predict the tokens to compose the name of the type 

In finetuning stage for ZFET, CA only masks the entity mentions and predicts their type names instead. For instance, given the context in Figure 1, we replace the entity mention `Northwest` with a `[MASK]` token and let CA module predict the name corporation of the target type `/organization/corporation` with a higher score. In more general cases, the length of a type name may exceed 1. Thus, the number of `[MASK]` tokens for replacement depends on the length of the type name (e.g., for type name living thing, we replace the corresponding mention with `[MASK]` `[MASK]`).

**Loss Function**

tl:dr - they average the probabilities of the tokens to predict (the ground-truth tokens) (averaged by the length of the type name) then optimize the $-\log p$ of all average probabilities

For each mention $m$ in the training set, we denote its ground-truth types as $T_{pos}$. For each type $t$ in $T_{pos}$, we replace $m$ with $l$ `[MASK]` tokens in the context of $m$, where $l$ is the length of $t$’s type name. We define the score $s_t$ and loss $l_t$ for type $t$ as $s_t = \frac{1}{|n_t|}\sum^{|n_t|}_{k=1}p_{n_{t,k}}$ $l_t = -\frac{1}{|n_t|}\sum^{|n_t|}_{k=1}\log p_{n_t,k}$ where $p_{n_{t,k}}$ is the probability for the $k$-th token of type name $n_t$ predicted by BERT. Considering all the types in $T_{pos}$, the overall loss for mention $m$ is $L_{m,CA} = \sum_{t \in T_{pos}} l_t$

#### Type Hierarchy-Aware (HA) Module

In HA module, we use Transformer encoder (Vaswani et al., 2017) with mask-self-attention to capture the hierarchical information for better type representations. Besides, we take the encoder from [[2019 Lin - An Attentive Fine-Grained Entity Typing Model with Latent Type Representation|Lin and Ji (2019)]] to learn the features of mentions and contexts. Then a similarity function is defined to compute the matching score between a mention and a candidate type based on the context.

Mention-Context encoder : based on ELMo [[Encoders - Neural Based Models - Attention based architectures]] 

**Hierarchy-Aware [[Models with Type Representations|Type Encoder]]**
Each type embedding is initialized using GloVe. Given a type to encode, a type type embedding matrix is composed by all initialized type embeddings (this matrix is frozen during the model training); a transformer (without the positional encoding) is trained to produce the type representation inside MSF. The self-attention mechanism inside the transformer is used to inject the hierarchy: *during the process of computing self-attention in Transformer encoder, a type only attends to its parent type in the hierarchy and itself, while the attention to the remaining types will be masked*

**Loss Function**
MSF CA and HA are optimized to obtain mention encoding similar to the correct type encodings.

Although the HA module does not directly learn any knowledge from instances of $T_{test}$, by encoding the type hierarchy $Ψ$ using mask-self-attention, Transformer encoder will capture the semantic correlation between types in $T_{train}$ and $T_{test}$, thus producing reliable representations for types in $T_{test}$.

#### Background Knowledge-Aware (KA) Module
We introduce prototypes and descriptions as two kinds of knowledge in the KA module.

- **Prototypes** refer to the carefully selected mentions for a type based on Normalized Point-wise Mutual Information (NPMI), which provide a mention-level summary for types [[2016 Ma - Label Embedding for Zero-shot Fine-grained Named Entity Typing|Ma et al., 2016]]. 
- **Descriptions** are queried from WordNet glosses (Miller, 1995) by type names, which provide a brief high-level summary for each type.

**Inference from Background Knowledge**
We hope to infer whether a mention $m$ matches a candidate type $t$, given the prototypes, type description and the context. In this work, we embody the KA module as natural language inference (NLI) from multiple premises (Lai et al., 2017). An example is presented in Figure 2, with input the same as Figure 1. We construct three premises corresponding to the context, prototypes and description respectively. The target hypothesis encodes that “the *type* is correct for the mention”. For both premises and hypothesis, we organize them into natural language sentences.

![[2021_chen_figure_2.png]]

An instance of CA is used to encode the premises and another instance is used to encode the hypotesis.

**Loss**
The loss is inspired from TransE, the intuition is that the sum of the premises encodings has to be as similar as possible as the hypothesis encoding

#### Inference

Given a test mention $m$ and a candidate type $t$ in $T_test$, we first compute the scores from each module: $s_t$ (by CA module), $y_t$ (by HA module) and $p_t$ (by KA module). Then we normalize them according to $x' = sigmoid(\frac{x - \mu_x}{sigma_x}), x\in{s_t, y_t, p_t}$
where $x$ is the score vector from a module for mention $m$ towards all types $t \in T_{test}$ with $x$ as component. $µ_x$ and $σ_x$ denote the mean and standard deviation of the vector $x$. The final decision score by our fusion model for type $t$ is: $score_t = \lambda_1 s'_t + \lambda_2 y'_t + \lambda_3 p'_t$ where $\lambda_1,\lambda_2,\lambda_3 \geq 0$ are hyper-parameters and $\lambda_1 +\lambda_2 + \lambda_3 = 1$.

#### Datasets
Experiments are carried on [[Dataset - Ren's BBN]] and [[Dataset - Ren's FIGER]] level-1 types are used as seen types and level-2 types are used as unseen (following [[2016 Ma - Label Embedding for Zero-shot Fine-grained Named Entity Typing|Ma et al (2016)]] setup)



---

Yi Chen 1 , 
Haiyun Jiang 1 , 
Lemao Liu 1 , 
Shuming Shi 1 , 
Chuang Fan Min Yang 2 , 
Ruifeng Xu 3

1 Tencent AI Lab, Shenzhen, China 
2 Shenzhen Institute of Advanced Technology, Chinese Academy of Sciences 
3 Peng Cheng Laboratory, Shenzhen, China

#paper #encoder_with_attention 