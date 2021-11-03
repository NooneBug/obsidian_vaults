https://aclanthology.org/D16-1144.pdf

Defines noise as [[Noise Definition - SIngle Path vs Multi-Path]], this definition has some problems [[Noise Definition Problems - Single Path vs Multi Path]]

In this paper, we approach the problem of automatic fine-grained entity typing as follows: 
	
	(1) Use different objectives to model training mentions with correct type labels and mentions with noisy labels, respectively. 
	(2) Design a novel partial-label loss to model true types within the noisy candidate type set which requires only the “best” candidate type to be relevant to the training mention, and progressively estimate the best type by leveraging various text features extracted for the mention. 
	(3) Derive type correlation based on two signals: 
		(i) the given type hierarchy, and 
		(ii) the shared entities between two types in KB, and incorporate the correlation so induced by enforcing adaptive margins between different types for mentions in the training set

The model is explained also as:

	1. Extract text features for entity mentions in training set M and test set Mt using their surface names as well as the contexts. (Sec. 3.1). 
	2. Partition training mentions M into a clean set (denoted as Mc) and a noisy set (denoted as Mn) based on their candidate type sets (Sec. 3.2). 
	3. Perform joint embedding of entity mentions M and type hierarchy Y into the same lowdimensional space where, in that space, close objects also share similar types (Secs. 3.3-3.6). 
	4. For each test mention m, estimate its type-path Y ∗ (on the hierarchy Y) in a top-down manner using the learned embeddings (Sec. 3.6).
	
So it is based on [[Encoders - Handcrated Features  Based Models]] and [[Ranking Loss]] : [[Ranking Loss - 2016 Ren - Partial Label Loss]], thus it is a [[Models Robust to Noise]]

Inference method is explained in [[Inference Method - Hierarchical Inference - 2016 Ren]]

The similarity between entity mention representation and type representations is computed using the dot product

AFET is eperimented on regenerated datasets, so on [[Dataset - Ren's FIGER]], [[Dataset - Ren's Ontonotes]] and on [[Dataset - Ren's BBN]]


#paper 