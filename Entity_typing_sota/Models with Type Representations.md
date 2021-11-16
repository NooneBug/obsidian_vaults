This Models represent types with vectors (or box embeddings) in order to represent similarities between them.

If the representations are computed at runtime, this can help the joint prediction  of two types that appear often in the same annotation because they will have also similar representation and probably the infer both them is easier. This kind of facility cannot be reached with flat classification modules. 

If the representations are computed runtime they can be biased by noise and/or training strategies

- The first paper that uses type representation in ET is [[2015 Yogatama - Embedding Methods for Fine Grained Entity Type Classification]]

- Then [[2016 Ma - Label Embedding for Zero-shot Fine-grained Named Entity Typing]] extends Yogatama's work introducing unseen label representation

- [[2016 Ren  - Label Noise Reduction in Entity Typing by Heterogeneous Partial-Label Embedding]] [[2016 Ren - AFET, Automatic Fine-Grained Entity Typing by Hierarchical Partial-Label Embedding]] [[2017 Abishek - Fine-Grained Entity Type Classification by Jointly Learning Representations and Label Embeddings]] learn runtime labels vectors and use dot product to produce a similarity score with the mention

- [[2017 Rabinovich - Fine-Grained Entity Typing with High-Multiplicity Assignments]] uses type cooccurrence and a Poset of types to encode types 

- [[2017 Shimaoka - Neural Architectures for Fine-grained Entity Type Classification]] uses a simple hierarchical representation: one-hot encodings contain a 1 on the i-esim dimension (to represent the i-esim type) and a 1 on each ancestor of the i-esim type

- [[2018 Zhang - Fine-grained Entity Typing through Increased Discourse Context and Adaptive Classification Thresholds]] learn runtime labels vectors and use cosine similarity to produce a similarity score with the mention

If the representations are pre-computed their quality can be checked before the training, also zero-shot learning is suitable

Approaches that use pre-computed type representation are:

- All approaches for [[Zero Shot Fine Grained Entity Typing]], otherwise the zero-shot will be impossible
- [[2019 Lopez - Fine-Grained Entity Typing in Hyperbolic Space]], which uses euclidean or hyperbolic space to embed hierarchical information about types