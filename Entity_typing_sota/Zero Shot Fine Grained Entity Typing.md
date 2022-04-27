Task proposed by [[2016 Ma - Label Embedding for Zero-shot Fine-grained Named Entity Typing]], consists in classical Entity Typing, but without examples for tested type

Is an extreme case of [[Few Shot Fine Grained Entity Typing]]

[[2016 Ma - Label Embedding for Zero-shot Fine-grained Named Entity Typing]] obtain prototypical embeddings for each type

[[2018 Yuan - OTyper , A Neural Architecture for Open Named Entity Typing]] represent types with word embeddings and learn to project entity mentions close to these embeddings; in this way, the types are not required to be known in advance

[[2018 Zhou - Zero-Shot Open Entity Typing as Type-Compatible Grounding]] uses freebase to train to extract a class given an entity mention; then given a dataset map the dataset types to Freebase classes and use the pretrained network to predict given the input. (I think that this is not zero-shot, since the network maybe has already seen a type. in [[2016 Ma - Zero-shot dataset partition]] , partition adopted by all other approaches, the network never sees some types.)  

[[2019 Obeidat - Description-Based Zero-shot Fine-Grained Entity Typing]] uses the type description available from Wikipedia to build a distributed semantic representation of the types.

[[2020 Ren - Neural Zero-Shot Fine-Grained Entity Typing]] For an entity type $t_k$ , we collect some example mentions of $t_k$ , the representation of an entity type $r_{t_k}$ is computed as the average of the embeddings of the words in these example mentions. For an entity which is present in training set, tens of example mentions can easily be manually sampled from training set, while for an entity type which is unseen in training set, we manually choose tens of example mentions to obtain the entity type representation. This simple yet effective method is motivated by [[2016 Ma - Label Embedding for Zero-shot Fine-grained Named Entity Typing|Ma et al 2016]] 

[[2021 Chen - An Empirical Study on Multiple Information Sources for Zero-Shot Fine-Grained Entity Typing]] types names are included in two different prompting NLI input, a third input is obtained by using the hierarchy to drive transformer's attention starting from GloVe Embedding.
