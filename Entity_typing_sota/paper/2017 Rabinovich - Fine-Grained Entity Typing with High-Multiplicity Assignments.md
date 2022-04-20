https://aclanthology.org/P17-2052.pdf

This work's use of a corpus exhibiting high type multiplicity with types derived from a semi-open inventory and its use of a fully structured model and decoding procedure, one that can in principle be integrated with neural models if desired. Previously, most results focused on the low-multiplicity Freebase-based FIGER corpus.

The models is based on "structured prediction", in order to model types as sets, each entity is assigned to a set of types that is a subset of all types

Entities are encoded through #encoder_with_handcrafted_features 

Types are encoded with two encoders based on:

	- type pair features (information about type cooccurrence)
	- a hierarchic graph (a Poset)
	
So this is a [[Models with Type Representations]]
	
The approach is evaluated with a new dataset (extracted from wikipedia) but no comparison with state of the art is performed

#paper #encoder_with_handcrafted_features 