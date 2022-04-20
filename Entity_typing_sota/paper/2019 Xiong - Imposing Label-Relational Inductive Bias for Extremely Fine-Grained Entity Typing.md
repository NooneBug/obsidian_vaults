https://aclanthology.org/N19-1084.pdf

*Existing entity typing systems usually exploit the type hierarchy provided by knowledge base (KB) schema to model label correlations and thus improve the overall performance. Such techniques, however, are not directly applicable to more open and practical scenarios where the type set is not restricted by KB schema and includes a vast number of free-form types. To model the underlying label correlations without access to manually annotated label structures, we introduce a novel label-relational inductive bias, represented by a graph propagation layer that effectively encodes both global label co-occurrence statistics and word-level similarities. On a large dataset with over 10,000 free-form types, the graph-enhanced model equipped with an attention-based matching module is able to achieve a much higher recall score while maintaining a high-level precision*

*To effectively capture the underlying label correlations without access to known type structures, we propose a novel label-relational inductive bias, represented by a graph propagation layer that operates in the latent label space. Specifically, this layer learns to incorporate a label affinity matrix derived from global type co-occurrence statistics and word-level type similarities. It can be seamlessly coupled with existing models and jointly updated with other model parameters*

- We impose an effective label-relational bias on entity typing models with an easy-to implement graph propagation layer, which allows the model to implicitly capture type dependencies;
- We augment our graph-enhanced model with an attention-based matching module, which constructs stronger interactions between the mention and context representations;
- Empirically, our model is able to offer significant improvements over previous models on the Ultra-Fine dataset and also reduces the cases of inconsistent type predictions

![[2019_xiong_architecture.png]]

The architecture is composed as follows:

- Words are represented with GloVe #pretrained_word_embeddings_glove  and positional embeddings
- Context is encoded with Bi-LSTM + self attention #encoders_with_recurrent_architecture  #encoder_with_attention 
- Entity mention is encoded with char CNN and self-attention
- Context and entity mention encodings are fed into a network with attention instead of being concatenated
- Type embeddings are extracted from the learned weight matrix for types [[Models with Type Representations]] enhanced with
	-  a graph derived representation, built using the type cooccurrence in the dataset and then applying GCN
	- a word derived representation based on average representation of GloVe vectors of types' names

Inference is made by optimizing the threshold value after the training

Experimented on [[Dataset - UFET]]

#paper #encoder_with_attention #encoders_with_recurrent_architecture 