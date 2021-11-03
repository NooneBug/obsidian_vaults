This Models represent types with vectors (or box embeddings) in order to represent similarities between them.

If the representatons are computed at runtime, this can help the joint prediction  of two types that appear often in the same annotation because they will have also similar representation and probably the infer both them is easier. This kind of facility cannot be reached with flat classification modules. 

If the representations are computed runtime they can be biased by noise and/or training strategies

The first paper that uses type representation in ET is [[2015 Yogatama - Embedding Methods for Fine Grained Entity Type Classification]]

Then [[2016 Ma - Label Embedding for Zero-shot Fine-grained Named Entity Typing]] extends Yogatama's work introducing unseen label representation

[[2016 Ren  - Label Noise Reduction in Entity Typing by Heterogeneous Partial-Label Embedding]] [[2016 Ren - AFET, Automatic Fine-Grained Entity Typing by Hierarchical Partial-Label Embedding]] [[2017 Abishek - Fine-Grained Entity Type Classification by Jointly Learning Representations and Label Embeddings]] learn runtime labels vectors and use dot product to produce a similarity score with the mention