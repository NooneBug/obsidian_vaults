https://aclanthology.org/2020.coling-main.7.pdf

https://github.com/TowerZhang/MZET


#### Abstract

With the growing size and granularity of the entity types, few previous researches concern with newly emerged entity types. 

In this paper, we propose MZET, a novel memory augmented FNET (Fine-grained NET) model, to tackle the unseen types in a zero-shot manner. MZET incorporates character-level, word-level, and contextual-level information to learn the entity mention representation. Besides, MZET considers the semantic meaning and the hierarchical structure into the entity type representation. 

Finally, through the memory component which models the relationship between the entity mention and the entity type, MZET transfers the knowledge from seen entity types to the zero-shot ones. 

#### Introduction

With the ever-growing number of entity types especially for fine-grained ones, it is difficult and expensive to collect sufficient annotations per category and retrain the whole model. Therefore, a zero-shot paradigm is welcomed in FNET to handle the increasing number of unseen types. The task we deal with in this paper is named zero-shot fine-grained named entity typing (ZFNET), which is to detect the unseen fine-grained entity types that have no labeled data available.

Learning generalizable representations for entity mentions and types is essential for the ZFNET task. Previous works learn these representations either from hand-crafted features (Ma et al., 2016; Yuan and Downey, 2018) or pre-trained word embeddings (Ren et al., 2016). These methods are insufficient and inefficient when challenged by poly-semantic, ambiguity, or even the newly-emerged mentions. The most recent works (Obeidat et al., 2019; Zhou et al., 2018) learn more informative but resource-costing representations by assembling the exterior Wikipedia knowledge base.

With the learned representations for entity mentions and entity types, most of the existing zero-shot FNET methods (Ma et al., 2016; Obeidat et al., 2019) project them into a shared semantic space. The shared space is learned through minimizing the distance between entity mentions and its corresponding seen entity types. In the prediction phase, testing entity mentions are classified to the nearest unseen entity types based on the assumption that the learned distance measurement also works for unseen types. These methods’ ability to transfer knowledge from seen types to unseen types is limited since they do not explicitly build connections between seen types and unseen types

In this work, we propose the memory augmented zero-shot FNET model (MZET) to tackle the aforementioned problems. MZET is designed to automatically extract the multi-information integrated mention representations and structure-aware semantic type representations with a large-scale pre-trained language model (Devlin et al., 2019). To effectively transfer knowledge from seen types to unseen types, MZET regards seen types as memory components and explicitly models the relationships between seen types and unseen types. Intuitively, we want to mimic the way how humans learn new concepts. Humans learn new concepts by comparing the similarities and differences between new concepts and old concepts stored in our memory

In summary, the main contributions of MZET are as follows. 
- We propose the memory augmented zero-shot FNET model (MZET) that can be trained in an end-to-end fashion. MZET extracts multi-information integrated mention representations and structure-aware semantic type representations without additional augmented data sources. 
- MZET regards seen types as memory components and explicitly models the relationships between seen types and unseen types to effectively transfer knowledge to new concepts. 
- MZET outperforms existing zero-shot FNET models significantly on the zero-shot fine-grained, coarse-grained, and hybrid-grained named entity typing over three benchmark datasets.

#### Proposed Model

The overview of the proposed MZET framework is illustrated in Figure 1. Specifically, MZET consists of three components: 
1) Zero-shot Memory Network that identifies entity types for entity mentions 
2) Mention Processor which extracts representation for entity mentions; 
3) Label Processor which obtains type representation

![[2020_zhang_zero_architecture.png]]

**3.1 Zero-Shot Memory Network** 
In the zero-shot entity typing task, there are no mentions available for these unseen entity types. Without the labeled data, we are not able to model the direct mapping from the new mentions to the new types. Here, we propose a novel zero-shot memory network that utilizes seen entity types to bridge the gap between the new mentions and the zero-shot entity types

**3.1.1 Memory augmented Typing Function** 

tl:dr literature simply compute the score of the input mention with respect to the inputed type (that can be unseen); instead, they compute an explicit score for each *seen type* using$MEM_{y_{seen}}$, that is simply a softmax over the scores on each seen type. They advocate that using seen types to favour the recognizement of unseen types remind the human process, also based on similarity w.r.t. previous knowledge.

To enable the zero-shot paradigm, previous researches (Ma et al., 2016; Obeidat et al., 2019) introduce a score function $f(·)$ to rate the match of a given entity mention $x$ and an entity type $y$, where $y$ is the raw type picked from $Y_{seen}$ or $Y_{unseen}$. The definition for $f(·)$ is: $f(x, y) = \Theta(A, x) \cdot \phi(y, B) = Ax \cdot By$ where $\Theta(x, A) : x \rightarrow Ax$ and $\phi(y, B) : y \rightarrow By$ serve as the mapping functions that project $x$ and $y$ into a shared semantic space by neural networks (ours are depicted in Sec. 3.2 and Sec.3.3 respectively). $f(·)$ is the distance estimation of $Ax$ and $By$ in the shared space 

Considering the lack of interpretability of the representations in the shared semantic space, we propose the memory network augmented zero-shot FNET to construct another high-level shared space, called **Association Space.** _Each dimension in the association space links to an entity type_. The representation in this space indicates the association information with each entity type. The score function for memory augmented zero-shot FNET is changed into $f'$ : $f'(x, y) = MEM_{y_{seen}}(\Theta(x, A), \phi(y, B)) = MEM_{y_{seen}}(Ax, By)$ where $MEM_{y_{seen}}(·)$ means rating score estimated by a memory network for the zero-shot paradigm with $Y_{seen}$ as the memory component. Meanwhile, the memory component is the aforementioned association space to guide unseen entity typing by linking them to each seen type stored in the memory components, like humans recognizing new things by intuitively associating with the knowledge they have memorized. In fact, $MEM_{y_{seen}}(·)$ loads $Ax$ and $By$ in the shared semantic space into the high-level association space, and then estimates matching score under the help of their connections to the seen types in the memory. 

**3.1.2 Zero-Shot Memory Network Model** 

tl:dr The representation of an unseen type in the association space is based on its similarities wrt seen types; similarities are computed applying a softmax on the euclidean distances between the unseen type representation, computed during the *zero-shot testing (???)* and the seen type representation, computed during the training

The key points to implement MEMYseen (·) are interpreted as follows: 
1) The Association Space is constructed with all the seen types representations to bridge the gap between mentions and unseen types. 
2) The mention representation is augmented by the association with seen types.
3) The augmented mention and type representation are projected into the Association Space. Association augmented mention can be directly project into it. But for the unseen types, associations between them with the seen types are formed by the type semantic similarity, which exactly presents each unseen type in the Association Space.

**3.2 Mention Processor**

Words in mention are represented in pretrained embeddings; to tackle out-of-vocabulary words char-level embedding is learnt at runtime using a Bi-LSTM. The concatenations of word and char embeddings are inputed in anther Bi-LSTM to extract and overall mention representation.

To obtain the context representation: a fixed window is used to cut the context surrounding the mention; then the cutted senttence (cutted left context, mention, cutted right context) is inputed to BERT. Each output token is inputed in a Bi-LSTM with attention #encoder_with_attention #encoders_with_recurrent_architecture 

The final mention representation is the concatenation of char, mention and context embedding

**3.3 Label Processor**

Label name is inputed to BERT to obtain a word level representation. Following [[2016 Ma - Label Embedding for Zero-shot Fine-grained Named Entity Typing|Ma et al 2016]], in the Label Processor they integrate the semantic embeddings of the child label and its parent label into a single embedding vector as the fine-grained label representation. To do this, they perform the dot product of the BERT-based embeddings with a binary hierarchical matrix that explicitly represents the hierarchy (1 on label index and 1 on ancestor indexes) 

**3.4 Loss Function**

Max-margin loss is used to rank correct mention-type pairs higher than wrong ones

**4 Datasets**

Experiments are carried out on [[Dataset - Ren's Ontonotes]], [[Dataset - Ren's BBN]] and [[Dataset - Ren's FIGER]] following [[2016 Ma - Zero-shot dataset partition|Ma et al 2016]] partition (leaves = unseen, non-leaves = seen)





---


Code: https://github.com/TowerZhang/MZET

Tao Zhang 1 , 
Congying Xia 1 , 
Chun-Ta Lu 2 , 
Philip S. Yu 1 

1 University of Illinois at Chicago, Chicago, IL, USA; 
2 Google Research, Mountain view, CA, USA

#paper