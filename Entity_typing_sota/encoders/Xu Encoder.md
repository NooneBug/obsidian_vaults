Encoder used firstly in [[2018 Xu - Neural Fine-Grained Entity Type Classification with Hierarchy-Aware Loss]] and then in other papers (linked to this note)

This approach represent words with #pretrained_word_embeddings_glove  (GloVe)

- Mentions are represented by averaging #pretrained_word_embeddings_glove  and also by LSTM #encoders_with_recurrent_architecture 

- Contexts are represented through Bi-LSTM over word vectors #encoders_with_recurrent_architecture #pretrained_word_embeddings_glove  and word level attention #encoder_with_attention 