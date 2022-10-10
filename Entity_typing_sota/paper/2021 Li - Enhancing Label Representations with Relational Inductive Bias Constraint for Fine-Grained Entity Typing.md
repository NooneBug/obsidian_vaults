https://www.ijcai.org/proceedings/2021/0529.pdf

## Methodology 
The proposed method consists of three main components: **mention features extractor, instance-aware label encoder, and pseudo-label generator**, as shown in Figure 2. The mention features extractor encodes the mention span and its context via attention mechanism to get context-aware mention representation. For the instance-aware label encoder, we design a two-phase heterogeneous graph to extract the learned features from instances to labels and then capture the dependency relationships among labels. During prediction, we employ the pseudo-label generator to generate pseudo labels for the testing instances to assist in constructing the two-phase graph. 

![[2021_li_figure_2.png]]

### 3.1 Mention Features Extractor 

tl:dr: Mention: ELMo -> Attention -> FFN; Context/Sentence : ELMo -> Transformer -> Attention

Given an example {m, c, y}, where m, c, y denote entity mention span, context, and ground truth labels, the mention features extractor is used to encode the context-aware representation of mention via encoding the mention span and its context respectively. Note that we define {m, c} as an instance here.

...

### 3.2 Instance-Aware Label Encoder

tl:dr: A dynamic graph is constructed: given a batch, a bipartite graph is defined, connecting instances to annotated labels. Instances representation is obtained by Mention Features Extractor (3.1). Label representations are random initialized. A **Graph Attention Network** is used to **estimate and use an attention matrix to propagate information** from **Instances Representations** in batch to **Label Representations** obtaining $t_{gat}$ (phase 1). Starting from $t_{gat}$ A GCN is used to propagate information between labels based on co-occurency in the dataset obtaining $t_{gcn}$ (phase 2).

Classification is operated through a dot product between the output of 3.1 and $T = T_{gcn} + T_{gat}$



## Old

Fine-Grained Entity Typing (FGET) is a task that aims at classifying an entity mention into a wide range of entity label types. Recent researches improve the task performance by imposing the labelrelational inductive bias based on the hierarchy of labels or label co-occurrence graph. However, they usually overlook explicit interactions between instances and labels which may limit the capability of label representations. Therefore, we propose a novel method based on a two-phase graph network for the FGET task to enhance the label representations, via imposing the relational inductive biases of instance-to-label and label-to-label. In the phase I, instance features will be introduced into label representations to make the label representations more representative. In the phase II, interactions of labels will capture dependency relationships among them thus make label representations more smooth. During prediction, we introduce a pseudo-label generator for the construction of the two-phase graph. The input instances differ from batch to batch so that the label representations are dynamic. Experiments on three public datasets verify the effectiveness and stability of our proposed method and achieve stateof-the-art results on their testing sets.

Experimented on [[Dataset - Ren's BBN]], [[Dataset - Ren's Ontonotes]] [[Dataset - Ren's FIGER]]

#todo #paper 