A kind of noise in entity typing defined by [[2018 Xu - Neural Fine-Grained Entity Type Classification with Hierarchy-Aware Loss]]. Out-of-context noise happens when an entity is annotated with correct types, but unrelated to the context

Example:

On May 14, 2014, Kerr reached an agreement to become the head coach for the Golden State Warriors, succeeding Mark Jackon 

Annotations for "Kerr": Person, Athlete, Coach. 

In this annotations, Athlete is an out-of-context noise, since cannot be inferred by the context

A particular kind of this noise is [[Noise Definition - Overly Specific]] noise, in which types not only are unrelated with the context, but finer than all types related to the context