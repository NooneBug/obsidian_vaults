https://aclanthology.org/W16-1313.pdf

*"In this work we propose a novel attentionbased neural network model for the task of fine-grained entity type classification that unlike previously proposed models recursively composes representations of entity mention contexts."*

So work based on #encoders_with_recurrent_architecture , [[Encoders - Sentence splitting]]

Uses Glove for word embeddings #pretrained_word_embeddings_glove

First method which uses attention

Given an entity mention within its sentence, the sentence is splitted [[Encoders - Sentence splitting]] then :

	- Mention is encoded by performing arithmetic mean on its word vectors
	- Context are separetly encoded using LSTM and attention
	- Mention and Context encodings are concatenated and fed into a Logistic Regression Layer
	
This methods produces [[Predictions - Multiple Path Precition]] and [[Predictions - Partial Path Prediction]]

Experimented on [[Dataset - FIGER]]



#paper #encoders_with_recurrent_architecture #pretrained_word_embeddings_glove 