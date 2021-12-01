Internal Hierarchy of [[2020 Chen - Hierarchical Entity Typing via Multi-level Learning to Rank]]

The representation is twofold:

-	The classification task is fashioned as a learning-to-rank task, but it is optimized to rank each true type higher than its sibling, using a level-threshold (so a different threshold depending by the abstraction level of the true type)
-	From the level 2, the level-threshold is set as the similarity with the parent, in this way the prediction is forced to respect the hierarchy  