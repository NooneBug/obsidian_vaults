This Models represent types with vectors (or box embeddings) in order to represent similarities between them.

If the representations are computed at runtime, this can help the joint prediction of two types that appear often in the same annotation because they will have also similar representation and probably the infer both them is easier. This kind of facility cannot be reached with flat classification modules. 

If the representations are computed runtime they can be biased by noise and/or training strategies

- The first paper that uses type representation in ET is [[2015 Yogatama - Embedding Methods for Fine Grained Entity Type Classification]]
- Then [[2016 Ma - Label Embedding for Zero-shot Fine-grained Named Entity Typing]] extends Yogatama's work introducing unseen label representation
- [[2015 Yogatama - Embedding Methods for Fine Grained Entity Type Classification]], [[2019 Dai - Improving Fine-grained Entity Typing with Entity Linking]], [[2020 Chen - Hierarchical Entity Typing via Multi-level Learning to Rank]],  simply optimize the type representations to maximize the dot product with the entity representation
- [[2016 Ren  - Label Noise Reduction in Entity Typing by Heterogeneous Partial-Label Embedding]], [[2016 Ren - AFET, Automatic Fine-Grained Entity Typing by Hierarchical Partial-Label Embedding]], [[2017 Abishek - Fine-Grained Entity Type Classification by Jointly Learning Representations and Label Embeddings]] learn runtime labels vectors and use dot product to produce a similarity score with the mention
- [[2017 Rabinovich - Fine-Grained Entity Typing with High-Multiplicity Assignments]] uses type cooccurrence and a Poset of types to encode types 
- [[2017 Shimaoka - Neural Architectures for Fine-grained Entity Type Classification]] uses a simple hierarchical representation: one-hot encodings contain a 1 on the i-esim dimension (to represent the i-esim type) and a 1 on each ancestor of the i-esim type
- [[2018 Xu - Neural Fine-Grained Entity Type Classification with Hierarchy-Aware Loss]] learn runtime type embeddings exactly like Yogatama
- [[2018 Zhang - Path-Based Attention Neural Model for Fine-Grained Entity Typing]] learn runtime labels vectors and sum them according to the hierarchy. The single type is represented by its embedding summed to all its ancestor embeddings
- [[2018 Zhang - Fine-grained Entity Typing through Increased Discourse Context and Adaptive Classification Thresholds]] learn runtime labels vectors and use cosine similarity to produce a similarity score with the mention
- [[2019 Lin - An Attentive Fine-Grained Entity Typing Model with Latent Type Representation]] learn runtime labels vectors and use a linear layer to produce a similarity score with the mention
- [[2019 Xin - Put It Back, Entity Typing with Language Model Enhancement]] each type is represented with a learnable vector, initialized with the word embedding of the type's label. 
- [[2019 Xiong - Imposing Label-Relational Inductive Bias for Extremely Fine-Grained Entity Typing]] represent co-occurrences with a graph and apply graph convolution network and GloVe to extract the type representation based on cooccurrence and word embeddings.
- [[2020 Shi - Alleviate Dataset Shift Problem in Fine-grained Entity Typing with Virtual Adversarial Training]] learn runtime representations and use them in the loss
- [[2021 Onoe - Modeling Fine-Grained Entity Types with Box Embeddings]]: represent each type with box
- [[2021 Qian - Fine-grained Entity Typing without Knowledge Base]] uses [[2019 Lin - An Attentive Fine-Grained Entity Typing Model with Latent Type Representation|2019 Lin]] so also uses type representation.
- [[2021 Selvaraj - Cross-Lingual Fine-Grained Entity Typing]] similar to [[2019 Onoe - Learning to Denoise Distantly-Labeled Data for Entity Typing]], so learn type representations

If the representations are pre-computed (using GloVe, word2vec, ELMo or BERT) their quality can be checked before the training, also zero-shot learning is suitable

Approaches that use pre-computed type representation are:

- All approaches for [[Zero Shot Fine Grained Entity Typing]], otherwise the zero-shot will be impossible
	- [[2016 Ma - Label Embedding for Zero-shot Fine-grained Named Entity Typing]]
	- [[2018 Yuan - OTyper , A Neural Architecture for Open Named Entity Typing]] represents types with word embeddings and map entity representation into the word space
	- [[2019 Obeidat - Description-Based Zero-shot Fine-Grained Entity Typing]] represents types starting from wikipedia description and project them in a common space for training / inference
	- [[2020 Ren - Neural Zero-Shot Fine-Grained Entity Typing]] types are represented by their glove representation and a type-attention matrix is learnt runtime
	- [[2020 Zhang - MZET, Memory Augmented Zero-Shot Fine-grained Named Entity Typing]] types are represented using BERT representations, combined using the hierarchy
	- [[2021 Weber - Zero-Shot Cross-Lingual Transfer is a Hard Baseline to Beat in German Fine-Grained Entity Typing]]
- [[2019 Lopez - Fine-Grained Entity Typing in Hyperbolic Space]], which uses euclidean or hyperbolic space to embed hierarchical information about types
- [[2019 Wu - Modeling Noisy Hierarchical Types in Fine-Grained Entity Typing, A Content-Based Weighting Approach]], uses a sum of the words of the type and all words of its ancestors

