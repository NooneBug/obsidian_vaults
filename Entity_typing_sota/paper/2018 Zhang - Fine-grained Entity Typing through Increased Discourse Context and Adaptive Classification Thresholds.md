https://aclanthology.org/S18-2022.pdf

![[2018_xin_architeture.png]]

*We propose a neural architecture (Figure) which learns more context-aware representations by using a better attention mechanism and taking advantage of semantic discourse information available in both the document as well as sentence-level contexts*

*We find that adaptive classification thresholds leads to further improvements*

Authors propose a model with three encoders:

- Entity Encoder: average of embedding of all word vectors #pretrained_word_embeddings_glove 
- Sentence Level Encoder:  Bi-LSTM on the sentence #encoders_with_recurrent_architecture with Attention #encoder_with_attention 
- Document-level Context Encoder: Multi-Level perceptron (Le and Mikolov 2014)

The obtained encoding is compared with type embeddings [[Models with Type Representations]]

The approach is based on Adaptive Threshold, which uses adaptive threshold for each type

The approach is experimented on [[Dataset - Ren's Ontonotes]], [[Dataset - Ren's BBN]], [[Dataset - Ren's FIGER]]

#paper #encoder_with_attention #encoders_with_recurrent_architecture #pretrained_word_embeddings_glove 