A kind of noise in entity typing defined by [[2018 Xu - Neural Fine-Grained Entity Type Classification with Hierarchy-Aware Loss]]. This kind of noise happens when assigned types are not only unrelated with the context, but finer than all types related to the context

Example:

Kerr graduated from the University of Arizoza in 1988

Annotations for "Kerr": Person, Coach, Athlete

In this case, not only Coach and Athlete cannot be extracted from the context, but are also more specific than the only type that can be inferred, i.e. Person