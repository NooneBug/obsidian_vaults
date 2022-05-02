https://aclanthology.org/2021.emnlp-main.431.pdf

https://github.com/lemaoliu/fet-data

#### Abstract

Existing work on Fine-grained Entity Typing (FET) typically trains automatic models on the datasets obtained by using Knowledge Bases (KB) as distant supervision. However, the reliance on KB means this training setting can be hampered by the lack of or the incompleteness of the KB. To alleviate this limitation, we propose a novel setting for training FET models: FET without accessing any knowledge base. Under this setting, we propose a two-step framework to train FET models. In the first step, we automatically create pseudo data with fine-grained labels from a large unlabeled dataset. Then a neural network model is trained based on the pseudo data, either in an unsupervised way or using self-training under the weak guidance from a coarse-grained Named Entity Recognition (NER) model. Experimental results show that our method achieves competitive performance with respect to the models trained on the original KB-supervised datasets

#### Introduction

A major challenge in fine-grained entity typing (FET) is the absence of human-annotated data. To address this problem, a common practice is to seek distant supervision from knowledge bases. Typically, the training data is obtained by linking entity mentions and drawing their types from knowledge bases. For example, Ling and Weld (2012) utilize the information encoded in anchor links from Wikipedia text along with the type information in Freebase (Bollacker et al., 2008). After that, classification models are trained using the resultant FET dataset. Despite its success, this framework has one limitation: The type ontology for training and testing is strongly restricted by the underlying KB. As a result, the application of the trained models under this framework can be hampered by the lack or the incompleteness of the KB (from Choi et al., 2018). In real-world applications of FET, the ontology of the fine-grained types depends on the applications instead of the KB. Typically, there may not exist a one-to-one mapping from the ontology of applications to that of the existing KB. For example, a game-related application may need to identify the named entities of some specific video games, such as the heroes and items in DOTA 2. However, there are no knowledge bases covering these named entities. The existing FET framework can not be used when the desired type topology is not compatible with any KB. Worse than this, large-scale knowledge bases are even not available in some languages. As a result, the trained FET classifiers under this framework cannot be effectively applied to real-word applications.

To lift this limitation, we study a novel FET setting, **fine-grained entity typing without a knowledge base**, which is a common setting in real-world applications. Given a fine-grained type ontology defined by an application, **we aim to assign a list of labels for each mention within an input sentence, yet without accessing any knowledge base**. Under this setting, we propose a novel FET framework by leveraging a large unlabeled dataset. Our proposed framework disentangles the type ontology from the KB and thus the given ontology can be an arbitrary one, defined by a practical application that does not correspond to any KB or by a specific KB as the conventional FET setting. Therefore, our proposed framework is more flexible than the previous one.

We propose an automatic method using Hearst patterns (Hearst, 1992) to achieve this goal. There exists a difference between the pseudo data and the testing data in that each sentence in the pseudo data satisfies a (relaxed) Hearst pattern while few testing data do. Consequently, directly training a FET model on the pseudo data may limit its generalization ability. We thereby propose a self-training method with weak supervision from a coarse-grained NER model in the second step to alleviate this issue. We do not focus on designing novel models under the conventional FET setting in this work. Actually, our proposed two-step framework does not set a limit on the backbone FET models and existing FET models can be freely migrated to our framework. Experimental results show that without utilizing any KB in the conventional framework, our proposed framework achieves comparable results to the conventional framework using the same backbone FET model.

Main contributions of our work are: 
	- We study fine-grained entity typing based on a new setting: FET without a knowledge base.
	- Under the new setting, we propose a two-step approach (pseudo data generation and model training) to tackle the FET task. 
	- Compared with training on KB-supervised datasets, our proposed approach achieves competitive performance on two popular FET testing datasets. 
	- To facilitate future research under this new setting, we make the created data publicly available

#### Related work
Related work is complete well done

#### Problem Statement for FETw/oKB 

*tl:dr: authors assume to have a type hierarchy in which each type is associated with a set of vocabs, forming a vocabulary; a FET network has to produce a subset of the vocabulary. They states that all literature approaches use datasets built with distant supervision to train the FET network, instead they want to be independent from the KB and so from the distant supervision annotations.*    

Suppose $L$ is a fine-grained entity type ontology for a real-world application as illustrated in Figure 2, which consists of a set of formal types organized as hierarchical trees, and a dictionary used to explain each node in the trees. Each node in a tree is a formal entity type l and each directed edge $(l_1, l_2)$ in the tree indicates that $l_2$ is a subtype of $l_1$. Each element in the dictionary consists of a formal type (i.e., a node) and a list of informal type names explaining the meaning of the formal type. Figure 2 shows an example, where the type names of the type `/organization/company` is the list `[company, enterprises, companies, enterprise]` and the type names of `/disease` is the list `[disease, illnesses]`. The generic FET task aims to predict the type set $T$ whose element is in the given ontology $L$. Note that $T$ may be a set with one or more type labels, so this task is characterized as a multi-class multilabel classification task. Formally, the FET task is modeled by a probabilistic model $P(l | x, c)$. A common practice is to parameterize the probabilistic model by a binary classifier $P_{\theta}(l | x, c)$, which indicates whether $l$ is a type label of the mention $x$. During inference, the classifier outputs all the labels l satisfying the condition $P_{\theta}(l | x, c) \geq 0.5$. **In the conventional framework, $\theta$ is trained on a distantly supervised dataset, which is dependent on a knowledge base. As a result, the trained classifier can only predict the types corresponding to the types in that knowledge base, limiting its application in practice.**

**Problem Statement** 
In this paper, we focus on FET under a more practical setting, i.e. Fine-grained Entity Typing without Knowledge Base (FETw/oKB). That is, given an ontology L, we aim to infer the type set T for the mention x within a sentence c when there are no KBs available. 
**Relation to Zero-shot FET** 
Suppose the type ontology L is divided into two disjoint sub-ontology L1 and L2, and there is a labeled training dataset where the labels are all from L1. Zero-shot FET aims to make a prediction on testing mentions whose labels are within L2. A surge of efforts have been devoted to zero-shot FET (Ma et al., 2016; Xian et al., 2019; Ren et al., 2020; Chen et al., 2021), but all of them assume that training data is obtained from knowledge bases by distant supervision, similar to the conventional FET. Therefore, the proposed FETw/oKB is clearly different from zero-shot FET

**Road Map** 
Generally, it is challenging to train $\theta$ under the FETw/oKB setting. In the next sections, we propose a new framework to address FETw/oKB. Its key idea is a two-step approach: 
- We propose an automatic method to create pseudo data from a large-scale unlabeled corpus (§4). 
- We propose a method to train the classifier by leveraging the pseudo data (§5).

**Pseudo Data from Scratch**

![[2021_Qian_general_idea.png]]

We start from the ontology L given by a real-world application, and our purpose is to create a large pseudo dataset with fine-grained labels from massive unstructured data. To this end, we propose an automatic method to achieve this goal without manual labor. At a high level, the key idea of our method is illustrated in Figure 2. In the next, we describe the key steps within our method.

#### 4.1 Dictionary Generation 

tl:dr, they use Hearst patterns to generate pairs of `(mention, type name)`, then cluster the pairs using similarity on mention, hierarhical clustering and cluster merging, obtaining clusters (i.e. lists of mentions) and a label name for them (e.g., `[Apple, Microsoft, Google, Facebook, ...]` is mapped to `company`) 

**Extraction** 
First, we use Hearst patterns (Hearst, 1992) to generate a mapping dictionary between mentions and type names. Each pattern corresponds to a relationship between a hypernym and a hyponym. For example, the patterns include “NP such as NP” and “NP is a NP”. Using these patterns to filter the unstructured data, we collect a large-scale text corpus consisting of sentences such as *“An apple is an edible fruit.”* and *“Apple is a high-tech company.”*. Along with the corpus, we also collect a large number of (mention, type name) pairs such as (apple, fruit), (Apple, company), (banana, fruit), and (Microsoft, company). We denote this set of `(mention, type name)` as $S$. 

**Clustering** 
There might be some pairs in $S$, which share the same mention but have different type names. Such a mention is an **ambiguous mention**. For example, *“apple”* is an ambiguous mention, because both of the type names, *“company”* and *“fruit”*, can be mapped to it. To resolve this problem, **we cluster all mentions in $M$ by an overlapping clustering algorithm and then assign a type name to each mention cluster**, whose meaning may be less ambiguous. 

Standard overlapping clustering algorithms either need to pre-define the number of clusters or are inefficient (Jain et al., 1999). Instead, we design a new algorithm whose basic idea includes three steps: 
- for each mention, it computes its neighbor set consisting of its top $k$ mentions according to a term similarity score; 
- a hierarchical clustering algorithm (Brown et al., 1992) is applied to each neighbor set, leading to many small subsets in total; 
- it repeatedly merges a pair of subsets to a larger subset according to a pre-defined threshold and finally take all subsets as clusters. 

Since one neighbor set may overlap with another one, the resulted clusters can be overlapping. According to the clusters, we create a map from mention clusters to type names. For example, the cluster `[Apple, Microsoft, Google, Facebook, ...]` is mapped to `company`. There are unambiguous mentions such as *“Google”* and *“Microsoft”* in this cluster, so the ambiguity of *“Apple”* can be reduced.

**4.2 Pseudo Data Generation by Matching & Mapping**

tl:dr, they use the pairs generated in 4.1 to generate pseudo-label for the mentions: if the mention appear in a cluster AND the type name appear in the context then the pseudo-label is generated. They argue that this can be seen as a relaxed Hearst Pattern

By using the cluster dictionary to match the corpus, we get our pseudo data. Take the sentence *“Recently Google has signed a contract with a popular company in Korea.”* as an example. The mention *“Google”* appears in the cluster `[Microsoft, Apple, Google, ...]` and this cluster is mapped to the type name `company` by the dictionary. To further preserve high precision in the pseudo data, we perform a calibration strategy when matching: only if we find type name `company` in the context of *“Google”*, the example `([Recently, Google, has signed a contract with a popular company in Korea.], company)` will be accepted. In this step, the type name `company` will be used as a calibration to reduce ambiguity. The final step is to map the informal type name `company` to the formal type `/organization/company` in $L$ according to the ontology dictionary within $L$. Finally, we obtain pseudo examples such as `([Recently, Google, has signed a contract with a popular company in Korea.], /organization/company)`.

Due to the calibration strategy, each sentence in the pseudo data has some type name in it, such as `company` in the example above, which is strongly associated with the ground truth type label of the mention, such as `/organization/company` in the example above. Therefore, training models directly on the pseudo data can not result in an effective FET model. Instead, we mask the type name in the pseudo data when using it for training, which leads to about $+1$ F1 gains in our preliminary experiments.

It is worth mentioning that it is possible to generate pseudo data by only using Hearst patterns along with the ontology dictionary within $L$, which is much simpler than our proposed generation method. However, this simple generation method leads to limited data compared with ours, because it only extracts those sentences that strictly satisfy a Hearst pattern but ignores some high-quality sentences. Take *“Recently Google has signed a contract with a popular company in Korea.”* as an example, our method can match this sentence and identify an entity *“Google”* with labeled as `/organization/company` even if this sentence does not satisfy any Hearst patterns at all. In this sense, our generation method can be considered as a relaxed version of the Hearst pattern method.

**5 Self-Training via Weak Guidance**

tl:dr, the dataset with pseudolabel shows some differences with the test; thus, they use the pseudolabel to train an initial model $m$, then took a NER from Literature, pass all the unlabeled dataset into the NER obtaining mentions and coarse-grain labels; feed $m$ with the mentions extracted by the NER to obtain pseudolabel classification and filter the pseudolabel according to the coarse-grain labels obtained with the NER; in this way a new annotation is generated; this new annotated dataset is used to update $m$

Note that each sentence in the above pseudo data satisfies a relaxed Hearst pattern while few in the test dataset do. In other words, there exists a gap between the pseudo dataset and the testing dataset. Therefore, directly using the pseudo data for training may not result in a typing model with good generalization ability. 

To alleviate this problem, we use an off-the-shelf coarse-grained NER model to fill the gap and propose a weakly-guided self-training method. The basic idea is to use the coarse-grained NER model to identify the entity mentions in an input sentence, which are then fed into the fine-grained typing model for self-training. **Typically, a coarse-grained NER model can achieve both high precision and high recall on the task of identifying mention boundaries, so the missing mentions in the pseudo data can be found by it.** Besides the boundaries of entity mentions, the coarse-grained NER model also predicts a coarse-grained entity type for each mention, which is used as weak supervision in our method to improve the performance of the fine-grained typing model. 

Given the pseudo data $U^l$ obtained from Section 4, an unlabeled dataset $U$, the fine-grained typing model $P^e_θ$ , and the off-the-shelf coarse-grained NER model $P^o$ , the training process is as follows: 

![[2021_qian_pseudocode.png]]

For each sentence $c_i$ in $U$: 
1) Extract entity mentions and their coarse-grained types from $c_i$ using the coarse-grained NER model. The output $E_o$ is a set of $<x_o, t_o>$ pairs, where $x_o$ is an entity mention and $t_o$ is a coarse-grained type. (Line 5)
2) Feed each extracted mention into the current fine-grained typing model and get the fine-grained type prediction $T_e$. (Line 6-7)
3) Compare each predicted type $t_e \in T_e$ with to and consider all the subtypes of $t_o$ in $T_e$ as the fine-grained labels of $x_o$. Then we merge the new training example $<c_i , x_o, T'_e>$ into $U$. (Line 8-15)
4) Update the fine-grained typing model using the expanded pseudo data

#### Experiments

Approach is experimented on [[Dataset - Ren's FIGER]] and [[Dataset - Ren's Ontonotes]]

Since this is a paper on how to generate and use a pseudolabeled dataset, they do not proposed a FET model, but they used [[2016 Shimaoka - An Attentive Neural Architecture for Fine-grained Entity Type Classification|Shimaoka et al 2016]] and [[2019 Lin - An Attentive Fine-Grained Entity Typing Model with Latent Type Representation|Lin et al 2019]] as backbone FET models

The pseudolabeled dataset is extracted from wikipedia text, the NER model is: Yangming Li, Lemao Liu, and Shuming Shi. 2021b. Segmenting natural language sentences via lexical unit analysis, EMNLP 2021

#### Results

The results show that our method can be freely applied to different backbone FET models, and more advanced FET model architectures result in better performance

**Discussion on Complementarity**
We find that the supervised training data of Ontonotes have a long-tail distribution and the LatentNER model trained under the conventional framework does not perform well on the types with a relatively small number of training examples. Luckily, our collected pseudo data have the potential to alleviate the problem of insufficient supervised data. We select the types with less than 10 examples in the training dataset of Ontonotes. The Ontonotes training dataset only contains 112 examples of the selected types while there are 1,000 times more in our pseudo data. For each of the selected types, we randomly sample 100 examples from the pseudo data and manually annotate. if the example is correct. Using the annotations, we calculate the accuracy of the pseudo examples. The overall accuracy is 89%. Since the collection of pseudo data is automatic and the created data exhibits high accuracy, using our method to expand the long-tailed training dataset might be an efficient way to improve the model performance

---

Jing Qian 1 , 
Yibin Liu 2 , 
Lemao Liu 3 , 
Yangming Li 3 , 
Haiyun Jiang 3 , 
Haisong Zhang 3 , 
Shuming Shi 3

1 University of California, Santa Barbara 
2 Peking University 
3 Tencent AI Lab

#paper 