https://aclanthology.org/D15-1103.pdf

"We propose FINET, a system for detecting the types of named entities in short inputs—such as sentences or tweets—with respect to WordNet’s super fine-grained type system (16k types of organizations, persons and locations)."

"FINET addresses the above problems by first generating a set of type candidates using multiple extractors and then selecting the most appropriate type(s). To generate candidates, we make use of a sequence of extractors that range from explicit to highly implicit. Implicit extractors are only used when more explicit extractors fail to produce a good type. Our extractors are based on patterns, mention text, and verbal phrases. To additionally extract highly implicit types, we use word vectors (Mikolov et al., 2013) trained on a large unlabeled corpus to determine the types ofsimilar entities that appear in similar contexts. This extractor is comparable to KB methods discussed above, but is unsupervised, and takes as candidates the types frequent within the related entities and contexts"

Each extractor has a stopping condition, which we check whenever the extractor produced at least one type. When the stopping condition is met, we directly proceed to the type selection phase. The reasoning behind this approach is to bias FINET towards the most explicit types

First approach in using #pretrained_word_embeddings_word2vec

Evaluated on Name Entity Recognition / inedite datasets

(ndr very useful for Docebo)

#paper #pretrained_word_embeddings_word2vec 