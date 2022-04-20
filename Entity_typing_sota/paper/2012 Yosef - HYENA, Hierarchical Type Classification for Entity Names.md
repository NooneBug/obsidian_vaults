https://aclanthology.org/C12-2133.pdf

From Abstract: This paper addresses very fine-grained types organized in a hierarchical taxonomy, with several hundreds of types at different levels. We present HYENA for multi-label hierarchical classification.

From Contribution: This paper introduces HYENA (Hierarchical tYpe classification for Entity NAmes). HYENA is a multi-label classifier for entity types based on hierarchical taxonomies derived from WordNet (Fellbaum, 1998) or knowledge bases like YAGO (Suchanek et al., 2007) or Freebase (Bollacker et al., 2008). HYENA’s salient contributions are the following: 
	• the first method for entity-mention type classification that can handle multi-level type hierarchies with hundreds of types and multiple labels per mention; 
	• extensions to consider cross-evidence and constraints between different types, by developing a meta-classifier demonstrating the superiority of HYENA; 
	• experiments against state-of-the-art baselines, demonstrating the superiority of HYENA; 
	• an extrinsic study on boosting NED by harnessing type information.

Authors defines the dataset [[Dataset - YAGO505]]

Experiments on [[Dataset - FIGER]] and [[Dataset - Original BBN]]

Authors use #encoder_with_handcrafted_features  and SVM 

First paper to use a hierarchical inference method [[Inference Method - Hierarchical Inference - 2012 Josef]], so HYENA produces [[Predictions - Single Path Prediction]]

#paper #encoder_with_handcrafted_features 