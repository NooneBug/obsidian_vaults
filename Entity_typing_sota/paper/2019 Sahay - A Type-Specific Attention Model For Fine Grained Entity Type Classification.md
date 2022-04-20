https://www.researchgate.net/profile/Lovelu-Hassan/publication/347144760_A_Study_on_Development_of_PKL_Power/links/5fe43cb0a6fdccdcb8f73150/A-Study-on-Development-of-PKL-Power.pdf#page=75

*This paper discusses notable parts of significant methods that exist in the domain. In the process of researching these methods, we observed certain drawbacks in the current Fine Grained Entity Type Classification (FETC) methods. Ignoring local contextual linguistic information and ignoring type membership information of these contextual entities are two main drawbacks we have focused upon. We propose an approach that overcomes both these drawbacks by employing a Bi-Directional Short Term Memory (Bi-LSTM) network with a layer of “type-specific” attention*

The network is composed as:

- Pretrained word vectors are projected in lower dimension #pretrained_word_embeddings_glove 
- Mention representation is obtained by averaging mention tokens 
- context representation by [[2017 Shimaoka - Neural Architectures for Fine-grained Entity Type Classification]] network #encoders_with_recurrent_architecture  #encoder_with_attention 
- Type specific attention layer (the main contribution of this article)

Evaluated on [[Dataset - Ren's FIGER]]

#paper #encoder_with_attention #pretrained_word_embeddings_glove 