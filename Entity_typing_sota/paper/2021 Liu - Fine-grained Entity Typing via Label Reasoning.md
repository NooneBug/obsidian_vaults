https://aclanthology.org/2021.emnlp-main.378.pdf

https://github.com/loriqing/Label-Reasoning-Network
Abstract
---
In this paper, we argue that the implicitly entailed extrinsic and intrinsic dependencies between labels can provide critical knowledge to tackle the above challenges. To this end, we propose Label Reasoning Network(LRN), which sequentially reasons finegrained entity labels by discovering and exploiting label dependencies knowledge entailed in the data. Specifically, LRN utilizes an auto-regressive network to conduct deductive reasoning and a bipartite attribute graph to conduct inductive reasoning between labels, which can effectively model, learn and reason complex label dependencies in a sequence-toset, end-to-end manner.

Description
---
This paper proposes Label Reasoning Network (LRN), which uniformly models, learns and reasons both extrinsic and intrinsic label dependencies without given any predefined label structures. Specifically, LRN utilizes an auto-regressive network to conduct deductive reasoning and a bipartite attribute graph to conduct inductive reasoning between labels. Both of these two kinds of mechanisms are jointly applied to sequentially generate fine-grained labels in an end-to-end, sequence-to-set manner.

![[2021_liu_idea.png]]

Deductive reasoning for exploiting extrinsic dependencies and inductive reasoning for exploiting intrinsic dependencies. In our Seq2Set framework, the label dependency knowledge can be effectively modeled in the parameters of LRN, automatically learned from training data, and naturally exploited during the sequential label decoding process

Contributions
---
By decomposing labels into attributes and associating long tail labels with frequent labels, LRN can also effectively resolve the long tail label problem by leveraging their non-long tail attributes. Through jointly leveraging the extrinsic and intrinsic dependencies via deductive and inductive reasoning, LRN can effectively handle the massive label set of FET. Generally, our main contributions are: 
	- We propose Label Reasoning Network, which uniformly models, automatically learns and effectively reasons the complex dependencies between labels in an end-to-end manner. 
	- To capture extrinsic dependencies, LRN utilizes deductive reasoning to sequentially reason labels via an auto-regressive network. In this way, extrinsic dependencies are discovered and exploited without predefined label structures. 
	- To capture intrinsic dependencies, LRN utilizes inductive reasoning to reason labels via a bipartite attribute graph. By decomposing labels into attributes and associating long-tailed labels with frequent attributes, LRN can effectively reason long-tailed and even zero-shot labels

Architecture
---
![[2021_liu_architecture.png]]

This approach uses a [[Encoders - Neural Based Models - BERT Based Architectures |BERT Based Encoder]]

**Deductive reasoning for extrinsic label dependencies**
"*The deductive reasoning-based decoder sequentially generates labels based on both context and previous labels, e.g., “for his books" + person → writer and “record an album" + person → musician. In this way, a label is decoded by considering both context-based prediction and previous labels-based prediction*"

This intuition is defined with [[Encoders - Neural Based Models - Recurrent architectures |auto-regressive LSTM]] with [[Encoders - Neural Based Models - Attention based architectures |two kinds of attention]]: attention on context and attention on previous generated labels 

A vector is obtained from BERT, attentions and LSTMs, concatenated in a strange way (see the paper, maybe this is a parameter optimization) and the type with highest logit is taken as next predicted label. This label, together with the input (sentence + previous labels) will form the input for the next step of the auto-regressive function. To stop the process, also a special token \[EOS\]  can be generated as label.

**Inductive Reasoning for Intrinsic Label Dependencies**
A bipartite graph is built, with attributes and labels. The hidden state (the same of the previous section) is used to generate an activation FOR EACH attribute. Labels are predicted based on their attribute activations

The graph is built in two ways: 
- with BERT MLM (masked language model): by masking the entity mention in each sentence and taking the most probable non-stop words (all words over a threshold); these attributes are called context attributes
- with Stanza (maybe word expansion functionality): the entity mention is processed by Stanza and all non-stop words all taken; these  attributes are called entity attributes

Each attribute is related with the respective label by computing relatedness between vectors in GloVe

The attribute activation is computed by comparing the representation obtained through a linear starting from the encoded representation AND the word embedding of the attribute. The label activation is the sum of the respective attribute activations. A label is predicted if the activation is greater than a threshold.

Loss
---
Authors propose two losses, one for the Inductive Reasoning generated labels, another for the Deductive Reasoning generate labels.

For the loss of the deductive labels see the paper, the loss is linked to other literature notions that now (December 2021) I don't know - Manuel Vimercati

The loss for the inductive reasoning label is based on the labels scores: the scores of positive labels are to maximize, the others are to minimize.

Experiments
---

The approach is evaluated on [[Dataset - UFET]] and [[Dataset - Ren's Ontonotes]]
___
Qing Liu1,3 , 
Hongyu Lin1, 
Xinyan Xiao4 , 
Xianpei Han1,2, 
Le Sun1,2 , 
Hua Wu4 

1Chinese Information Processing Laboratory 
2State Key Laboratory of Computer Science Institute of Software, Chinese Academy of Sciences, Beijing, China 
3University of Chinese Academy of Sciences, Beijing, China 
4Baidu Inc., Beijing, China

#paper 