Proposed by [[2014 Gillick - Context-Dependent Fine-Grained Entity Type Tagging]]

The taxonomy was assembled manually using an iterative process, starting with FIGER nonhierarchical types. We organized the types into a hierarchy and then refined them, removing labels that seemed rare or ambiguous, and including new labels if there were enough examples to justify the addition. In general, we preferred a taxonomy that would yield a single label path for each mention and have as little ambiguity as possible. Once this process was finalized, we mapped the common (non-hierarchical) Freebase types to our types. Whenever there was any ambiguity in the mapping, we backed off to a common parent in the hierarchy. Finally, we note that the set of 505 YAGO types used in YAGO505 is also hierarchical, with 5 top-level types and 100 labels in each subcategory. Most of our types can be mapped to YAGO types in a straight-forward manner. However, we found that using the YAGO labels directly would lead to much ambiguity in manual annotations, primarily due to the large number of labels, the directed-acyclic-graph nature of the hierarchy, and the presence of ‘qualitative’ labels (e.g. person/good person, event/happening/beginning).

Train set is composed of 133,000 news documents, annotated with [[Distant Supervision]]

Test set includes all news documents in the [[Dataset - OntoNotes v1]] test set except the longest 4, which we dropped to reduce annotator burden

This dataset allows [[Predictions - Partial Path Prediction]] 

Performances can be found in [[Performances - Ontonotes v5 - GFT]]

#dataset #dataset_with_10_to_999_classes #dataset_with_hierarchical_set_of_types