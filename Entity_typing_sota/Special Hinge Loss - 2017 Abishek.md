[[2017 Abishek - Fine-Grained Entity Type Classification by Jointly Learning Representations and Label Embeddings]] discriminates between clean mentions (annotated with types that lies in a single path) and noisy mention (others)

So like [[Ranking Loss - 2016 Ren - Partial Label Loss]] uses two different hinge losses, 
a clean hinge losses in which mention representation has to have

	- similarity with positive type vectors > 1
	- similarity with negative type vectors < 1


and a noisy hinge losses in which mention representation has to have

	- similarity with ONE positive type vector > 1 (the one with maximum similarity)
	- similarity with negative type vectors < 1

This let the model to decide which types assign, obtaining a model which is robust to noise

