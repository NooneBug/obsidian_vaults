[[2016 Ren  - Label Noise Reduction in Entity Typing by Heterogeneous Partial-Label Embedding]] and [[2016 Ren - AFET, Automatic Fine-Grained Entity Typing by Hierarchical Partial-Label Embedding]] use:

	- given an entity mention representation and all types representations
	1 compute the similarity (dot product) with all coarse types representation
	2 select the highest one
	3 compute the similarity (dot product) with its sons (if there are some)
	4 repeat 2 and 3 until there are no more son or the highest similarity is lower than a threshold
	
#inference_method