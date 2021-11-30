https://arxiv.org/pdf/1803.03378.pdf

"Existing methods rely on distant supervision and are thus susceptible to noisy labels that can be out-of-context or overly-specific for the training sentence. Previous methods that attempt to address these issues do so with heuristics or with the help of hand-crafted features. Instead, we propose an end-to-end solution with a neural network model that uses a variant of crossentropy loss function to handle out-of-context labels, and hierarchical loss normalization to cope with overly-specific ones. Also, previous work solve FETC a multi-label classification followed by ad-hoc post-processing. In contrast, our solution is more elegant: we use public word embeddings to train a single-label that jointly learns representations for entity mentions and their context."

First paper that explicitly talking about [[Noise Definition - Out-of-context]] and [[Noise Definition - Overly Specific]]

Authors use [[Noise Definition - SIngle Path vs Multi-Path]], assuming that only single path types are to predict and so [[Dataset Modification - 2018 Xu - Multilabel to single label | casting the multilabel entity typing task in a single label task]], using the terminal node for each possible single-path and inferring the ancestors after. 

![[2018_xu_architecture.png]]

The encoder is [[Xu Encoder]]

Authors propose two different losses:

- A simple modification of the BCE to apply on Multi-Path examples: in this case, if the type with the max probability is one of the multi-path types, then is considered correct
- A hierarchy-aware loss: the probability of each type is raised by a fraction of the probability of all its ancestors (i.e. athlete has a probability composed by the one of athlete itself and a bit of the one of person)

This approach is experimented on [[Dataset - Ren's Ontonotes]] and [[Dataset - Ren's FIGER]]

#paper 