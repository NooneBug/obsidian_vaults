https://ww.sentic.net/label-embedding-for-zero-shot-named-entity-typing.pdf

*In this paper, we present a label embedding method that incorporates prototypical and hierarchical information to learn pre-trained label embeddings. In addition, we adapt a zero-shot framework that can predict both seen and previously unseen entity types. We perform evaluation on three benchmark datasets with two settings: **
	
	1) few-shots recognition where all types are covered by the training set;  
	2) zero-shot recognition where fine-grained types are assumed absent from training set. 
	
*Results show that prior knowledge encoded using our label embedding methods can significantly boost the performance of classification for both cases.*

This is the first work in [[Few Shot Fine Grained Entity Typing]] and [[Zero Shot Fine Grained Entity Typing]]

Author propose "a simple yet effective method for learning prototype-driven label embeddings that works for both seen and unseen types and is robust to the label noise. Another contribution of this work is that we combine prototypical and hierarchical information for learning label embeddings."

This work starts from [[2015 Yogatama - Embedding Methods for Fine Grained Entity Type Classification]] but substitutes one hot label encodings with label prototype vectors. This is a [[Models with Type Representations]]

Prototype vectors are obtained following these steps:

	1. Obtain Prototypical Word Vectors by performing the average of the vectors of headwords of entities that are instances of those labels
	2. Obtain the Hierarchical Label Embedding by building a binary vector for each label; the binary vector has 
		A. a number of dimension equal to the number of types
		B. a one in correspondance of the parent label
	3. For each label, multipli Prototypical Word Vector with Hierarchical Label Embedding

The learning is done in two setups:

	1. use word vectors as target and learn only the entity mention & sentence matrix
	2. use word vectors as starting point and learn both matrices (the one that projects the entity mention & sentence and the one that projects the label representation)
	
This method uses simple [[Ranking Loss]]

The inference method is explained in [[Inference Method - Hierarchical Inference - 2016 Ma]] 

The encoder is based on [[Encoders - Handcrafted Features  Based Models]]

The approach is evaluated on [[Dataset - Ren's BBN]], [[Dataset - Ren's FIGER]], [[Dataset - Ren's Ontonotes]] only for few shot and zero shot (and so it is not reported)

#paper 