https://arxiv.org/pdf/1906.02505.pdf

- We develop a fine-grained entity typing model that embeds both entity types and entity mentions in hyperbolic space. 
- We compare two different entity type hierarchies, one created by experts (WordNet) and one generated automatically, and find that their adequacy depends on the dataset. 
- We study the impact of replacing the Euclidean geometry with its hyperbolic counterpart in an entity typing model, finding that the improvements of the hyperbolic model are noticeable on ultra-fine types

![[2019_lopez_architecture.png]]

The architecture is:

- [[2017 Shimaoka - Neural Architectures for Fine-grained Entity Type Classification]] as input encoder
- Construct a graph that combines hierarchical information with cooccurrence information and then embed it obtaining a type representation [[Models with Type Representations]]
- Three projector to project input representation into the type representation space
	- Coarse projector to predict the coarse types, takes in input the input representation
	- Fine projector to predict the fine types, takes in input the input representation and the coarse projection
	- Ultra projector to predict the ultra fine types, takes in input the input representation and the fine representation
- The loss is a variation of the [[Losses - Choi Loss]] computed on the three representation and on the distance wrt type representation instead of computing on logistic values (like the original)

The approach is evaluated on [[Dataset - UFET]] and [[Dataset - Ren's Ontonotes]]
#paper 