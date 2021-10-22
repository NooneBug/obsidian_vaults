Rules applied by [[2014 Gillick - Context-Dependent Fine-Grained Entity Type Tagging]] on [[Dataset - Ontonotes v5]] training set to produce a denoised training corpus [[Denoising Techniques - Modify the training set]]. Rules are:

Sibling Pruning:

	1. Remove siblings types associated with a single entity, leaving only the parent type. The motivation for this heuristic is that it is uncommon for several sibling types to be relevant in the same context.

Coarse Type Pruning:
	
	2. Removes types that do not agree with the output of a standard coarse-grained type classifier trained on the set of types {person, location, organization, other}. We use a softmax classifier trained on labeled data derived from ACE (Doddington et al., 2004). We apply a simple label mapping to the four coarse types, and use features similar to those described in Klein et al. (2003). The motivation here is to reduce ambiguity by encouraging type labels to correspond to a single subtree of a hierarchy. Furthermore, if the entity is annotated with conflicting types (e.g. location and organization), this heuristic can help select the type more appropriate to the context.
	
Minimum Count Pruning: 

	3. The third heuristic removes types that appear fewer than some minimum number of times in the document (in our experiments, we require each type to appear at least twice)
	
#denoising_technique