https://arxiv.org/pdf/1909.12079.pdf

*In this paper, we use entity linking to help with the fine grained entity type classification process. We propose a deep neural model that makes predictions based on both the context and the information obtained from entity linking results*

*Our approach, when links the mention correctly, also uses all the types of the referred entity in KB as extra information. This may cause the trained model to overfit the weakly labeled data. We design a variant of the hinge loss and introduce noise during training to address this problem*

-	We propose a deep neural fine-grained entity typing model that utilizes type information from KB obtained through entity linking. 
-	We address the problem that our model may overfit the weakly labeled data by using a variant of the hinge-loss and introducing noise during training.

![[2019_dai_architecture.png]]

*Our FET approach is illustrated in Figure 1. It first constructs three representations: context representation, mention string representation, and KB type representation. Note that the KB type representation is obtained from a knowledge base through entity linking and is independent of the context of the mention*

The model is composed with the following modules:

- Context representation: BiLSTM over word vectors #encoders_with_recurrent_architecture #pretrained_word_embeddings_glove 
- Mention string representation: average of mention word vectors #pretrained_word_embeddings_glove 
- KB Type Representation: 
	- run an EL algorithm on the current example
	- if EL returns something, extract the types and return the onehot encodings of all extracted types (one vector)
- Linking score: the confidence score for the EL algorithm on this examples
- Type embedding is obtained in the same way as [[2015 Yogatama - Embedding Methods for Fine Grained Entity Type Classification]][[Models with Type Representations]]

A type is inferred if the dot product between the entity mention representation and the type representation is >0

KB Type Representation is perturbed to avoid the overfitting of the model on this representation

Authors use a variant of the [[Special Hinge Loss - 2017 Abishek]], simply the error is weighted based on the information about the EL, if one of the types from EL is a son of person, the loss will be amplified by a parameter  $\lambda$ . This choice is due to the observation that the networks tend to missclassify more  the sons of persons.

The approach is experimented on [[Dataset - Ren's FIGER]] and [[Dataset - Ren's BBN]]

#paper 
#entity_linking #encoders_with_recurrent_architecture #pretrained_word_embeddings_glove 