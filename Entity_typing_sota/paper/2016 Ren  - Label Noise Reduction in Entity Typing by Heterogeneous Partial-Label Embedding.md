https://arxiv.org/pdf/1602.05307.pdf

*Define a new task, Label Noise Reduction in Entity Typing (LNR), to be the automatic identification of correct type labels (type-paths) for training examples, given the set of candidate type labels obtained by [[Distant Supervision]] with a given type hierarchy. The unknown type labels for individual entity mentions and the semantic similarity between entity types pose unique challenges for solving the LNR task.*

Defines noise as [[Noise Definition - SIngle Path vs Multi-Path]], this definition has some problems [[Noise Definition Problems - Single Path vs Multi Path]]

We approach the LNR task as follows: 

	- (1) Model the true type labels in a candidate type set as latent variables and require only the “best” type (measured under the proposed metric) to be relevant to the mention—this requirement is less limiting compared with other multi-label learning methods that assume every candidate type is relevant to the mention. 
	- (2) Extract a variety of text features from entity mentions and their local contexts, and leverage corpuslevel co-occurrences between mentions and features to model mentions’ types. 
	- (3) Model type correlation (semantic similarity) jointly with mention-candidate type associations and mention-feature co-occurrences, to assist type-path inference, by exploiting two signals: 
		- (i) the given type hierarchy, and 
		- (ii) the shared entities between two types in KB.

So it is based on [[Encoders - Handcrated Features  Based Models]] and [[Ranking Loss]]

Inference method is explained in [[Inference Method - Hierarchical Inference - 2016 Ren]]

The method is designed as a graph embedding method, but is quite complicated; a clearer version is contained in [[2016 Ren - AFET, Automatic Fine-Grained Entity Typing by Hierarchical Partial-Label Embedding]]

#paper 