[[2016 Ren  - Label Noise Reduction in Entity Typing by Heterogeneous Partial-Label Embedding]] and [[2016 Ren - AFET, Automatic Fine-Grained Entity Typing by Hierarchical Partial-Label Embedding]]

Define noise as "Distant Supervision introduces label noise to the mentions since it fails to take the semantics of the mentions’ local contexts into account when assigning type labels"

This kind of noise depict the fact that a naif distant supervision system assigns all types once it found the link to the mention, disregarding the sentence in which the mention is placed

The basic idea is that when an entity mention is placed in a sentence, only a small set of its possible types has to be used; so the predicted types has to be coherent. In this paper a coherent set of label is a set of labels which lies on a single path in the tree hierarchy (starting from the root)

This definition has counterfactuals : [[Noise Definition Problems - Single Path vs Multi Path]]

There is a [[Noise Definition - Single Ancestor vs Multi Ancestor | lighter definition]]

	