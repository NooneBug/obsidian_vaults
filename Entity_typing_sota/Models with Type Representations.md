This Models represent types with vectors (or box embeddings) in order to represent similarities between them.

If the representaton are computed at runtime, this can help the joint prediction  of two types that appear often in the same annotation because they will have also similar representation and probably the infer both them is easier. This kind of facility cannot be reached with flat classification modules

The first paper that uses type representation in ET is [[2015 Yogatama - Embedding Methods for Fine Grained Entity Type Classification]]