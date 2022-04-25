https://dl.acm.org/doi/pdf/10.1145/3366424.3382725

#### Abstract

Due to the heavy work of human annotation, high quality training data is always not enough, zero-shot fine-grained entity typing becomes important. Previous zero-shot works rely on hand-crafted features and suffers from noisy distant supervision induced training data. 

In this paper, we propose a Neural Zero-Shot Fine-Grained Entity Typing (NZFET) model. NZFET is an end-to-end neural model free from hand-crafted features. The entity type attention in NZFET makes model focus on information relevent to the entity type. 

In our experiments, NZFET obtains better results on popular datasets than previous works. And we show experimentally that our method is robust against noisy training data.

#### Introduction
In the area of zero-shot fine-grained entity typing, only [[2016 Ma - Label Embedding for Zero-shot Fine-grained Named Entity Typing|Ma et al 2016]] conducts zero-shot fine-grained entity typing. However, their method needs hand-crafted features and is not very robust against noisy data. 

In this paper, we propose an end-to-end Neural Zero-Shot FineGrained Entity Typing (NZFET) model. It does not need handcrafted features. Moreover, NZFET employs attention with respect to entity types to make the model pay attention to context semantically relevant to the type, which makes the model more robust against noisy training data. NZFET is motivated by [[2016 Ma - Label Embedding for Zero-shot Fine-grained Named Entity Typing|Ma et al 2016]], however their model relies on hand-crafted features and the representation of the mention context is heavily affected by noisy data. 

Experiments show that NZFET outperforms existing zero-shot fine-grained entity typing methods and is more robust against noisy data.

#### Methodology 

![[2020_Ren_architecture.png]]

**Entity Type, Mention and Context Representations.** 

tl:dr - mention is represented as the average of embeddings of the words; context is represented by applying bi-LSTM with attention on the context; it is not clear how the type is represented, the paper starts talking about example mentions (the authors use the examples extracted by [[2016 Ma - Label Embedding for Zero-shot Fine-grained Named Entity Typing|Ma et al 2016]], but when the type representation is explained these example mentions are not mentioned but an attention method is explained (it is not clear if based on the input mention, as seems from figure 1, or based on the example mentions; based on the experiment section, examples are used to train the type attention network, then the network is applied on the input sentence at inference time)

---

For an entity type $t_k$ , we collect some example mentions of $t_k$ , the representation of an entity type $r_{t_k}$ is computed as the average of the embeddings of the words in these example mentions. For an entity which is present in training set, tens of example mentions can easily be manually sampled from training set, while for an entity type which is unseen in training set, we manually choose tens of example mentions to obtain the entity type representation. This simple yet effective method is motivated by [[2016 Ma - Label Embedding for Zero-shot Fine-grained Named Entity Typing|Ma et al 2016]] 

Supposing that the representation of a mention $m$ is $r_m$ ∈ $R^{D_w}$ . $r_m$ is computed as the average of the embeddings of the words in a mention $m$. 

We propose entity type attention to encode context information. We adopt a bidirectional LSTM whose hidden size is $D_h$. The word embeddings of the left and right context are fed into bi-LSTM to get hidden states $h^l_i$ and $h^r_i$. 

Then, each of entity type representations $r_{t_k}$ attends to each of the hidden state $h^l_i$ , $h^r_i$ to compute an scalar value $\hat a_{i,k}$ with a weight matrix $W \in R^{2D_a \times D_w}$ , which is expected to focus on relevant words to type $t_k$ . Then, these scalar values are normalized with softmax so that they sum to 1. The normalized scalar values of $\hat a_{i,k}$ is then denoted as $a_{i,k}$ which is the attention weight for each hidden state $h^l_i$ , $h^r_i$ . More precisely, $\hat a_{i,k}$ is computed as follows: $\hat a^l_{i,k} = h^{l^T}_i Wr_{t_k}$ .
$\hat a^r_{i,k}$ is computed the same as $\hat a^l_{i,k}$ . Then, the context representation with respect to entity type $t_k$ is calculated through weighted sum of hidden states. 

Previous fine-grained entity typing neural models with attention do not contain entity type information [2017 Shimaoka, 2017 Zhang]. Incorporating entity type representations into attention will help the model pay attention to semantic meanings which is beneficial to select the true entity types and be more robust to noisy training data which is prevalent in fine-grained entity typing.

**Optimization.** 

All representations are optimized through a ranking loss to rank the score of the positive examples higher than the score of negative examples; the score is the dot product between the type representation a learnt matrix A and the concatenation of mention and context representations.

#### Experiment
Experiments are conducted on [[Dataset - Ren's BBN]], [[Dataset - Ren's FIGER]] and [[Dataset - Ren's Ontonotes]]; for zero-shot the same [[2016 Ma - Zero-shot dataset partition|partition]] used by [[2016 Ma - Label Embedding for Zero-shot Fine-grained Named Entity Typing|Ma et al 2016]]


---

Yankun Ren 
Jianbin Lin 
Jun Zhou

Ant Financial Services Group Hangzhou, China