https://users.cs.northwestern.edu/~ddowney/publications/zheng_aaai_2018.pdf

*Classical NET targeted a few coarse-grained types, but the task has expanded to sets of hundreds of types in recent years. Existing work in NET assumes that the target types are specified in advance, and that hand-labeled examples of each type are available. In this work, we introduce the task of Open Named Entity Typing (ONET), which is NET when the set of target types is not known in advance. We propose a neural network architecture for ONET, called OTyper , and evaluate its ability to tag entities with types not seen in training*

This is an approach towards [[Zero Shot Fine Grained Entity Typing]], represent types with word embeddings and learn to project entity mentions close to these embeddings; in this way, the types are not required to be known in advance

![[2018_yuan_architecture.png]]

The network is composed as follows:

- Mention encoder: average of pretrained word vectors [[Encoders - Pretrained Word Embeddings]]
- Context encoder: two BiLSTM (one for left and one for right context) + attention [[Encoders - Neural Based Models - Recurrent architectures]] [[Encoders - Neural Based Models - Attention based architectures]]
- Features: other handcrafted features are added to the input representation
- Type Embeddings: average of pretrained word vectors that form the type name [[Encoders - Pretrained Word Embeddings]]

Method is experimented on [[Dataset - Ren's FIGER]] and a disambiguation dataset

#paper 