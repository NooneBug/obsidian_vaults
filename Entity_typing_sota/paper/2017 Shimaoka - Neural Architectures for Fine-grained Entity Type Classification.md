https://aclanthology.org/E17-1119.pdf

"we investigate several neural network architectures for fine-grained entity type classification and make three key contributions. Despite being a natural comparison and addition, previous work on attentive neural architectures have not considered hand-crafted features and we combine these with learnt features and establish that they complement each other. Additionally, through quantitative analysis we establish that the attention mechanism learns to attend over syntactic heads and the phrase containing the mention, both of which are known to be strong hand-crafted features for our task. We introduce parameter sharing between labels through a hierarchical encoding method, that in low dimensional projections show clear clusters for each type hierarchy"

This is the first model that uses together handcrafted features and neural encoders with attention. #encoder_with_handcrafted_features #encoders_with_recurrent_architecture  #encoder_with_attention

In this paper different mention encoding architectures are experimented, all starting from GloVe #pretrained_word_embeddings_glove  to represent single words: 

The mention can be represented with:

	- average of vectors
	- handcrafted features
	
The context can be represented with:

	- average of vectors
	- LSTM on vectors
	- Bi-LSTM with attention on vectors

Also an hybrid model is presented:

	- both handcrafted and average for mention and Bi-LSTM representations for context

A simple hierarchical representation for type is proposed: one-hot encodings contain a 1 on the i-esim dimension (to represent the i-esim type) and a 1 on each ancestor of the i-esim type. This can be considered as a [[Models with Type Representations]]

Uses the same inference method as [[2016 Shimaoka - An Attentive Neural Architecture for Fine-grained Entity Type Classification]] : [[Inference Method - Threshold or Max]]

The approaches are evaluated on Ren's Datasets: [[Dataset - Ren's FIGER]] [[Dataset - Ren's Ontonotes]] but also [[Dataset - FIGER]] and [[Dataset - Ontonotes v5 - GFT]]


#paper #encoder_with_handcrafted_features #encoder_with_attention #encoders_with_recurrent_architecture #pretrained_word_embeddings_glove 