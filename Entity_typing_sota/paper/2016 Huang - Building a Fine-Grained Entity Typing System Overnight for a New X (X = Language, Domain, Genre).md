https://arxiv.org/pdf/1603.03112.pdf

*In this paper, we propose a novel unsupervised entity typing framework by combining symbolic and distributional semantics. We start from learning general embeddings for each entity mention, compose the embeddings of specific contexts using linguistic structures, link the mention to knowledge bases and learn its related knowledge representations. Then we develop a novel joint hierarchical clustering and linking algorithm to type all mentions using these representations. This framework doesn’t rely on any annotated data, predefined typing schema, or hand-crafted features, therefore it can be quickly adapted to a new domain, genre and language. Furthermore, it has great flexibility at incorporating linguistic structures (e.g., Abstract Meaning Representation (AMR), dependency relations) to improve specific context representation. Experiments on genres (news and discussion forum) show comparable performance with state-of-the-art supervised typing systems trained from a large amount of labeled data. Results on various languages (English, Chinese, Japanese, Hausa, and Yoruba) and domains (general and biomedical) demonstrate the portability of our framework*

This work is base on Heuristic: 

Heuristic 1: The types of common entities can be effectively captured by their general semantics.

Heuristic 2: The types of uncommon, novel, emerging, and polysemantic entities can be inferred by their specific contexts.

Heuristic 3: The types of domain specific entities largely depend on domain-specific knowledge.

*For the first time, we propose an unsupervised finegrained entity typing framework that combines general entity semantics, specific contexts, and domain specific knowledge. Without the needs of predefined typing schema, manual annotations and hand-crafted linguistic features, this framework can be easily applied to new domains, genres, or languages. The types of all entity mentions are automatically discovered based on a set of clusters, which can capture fine-grained types customized for any input corpus. We compare the performance of our approach with state-ofthe-art name tagging and fine-grained entity typing methods, and show the performance on various domains, genres, and languages.*

	- We present an unsupervised entity typing framework that requires no pre-defined types or annotated data. Instead, it can automatically discover a set of fine-grained types customized for the input corpus
	- We combine three kinds of representations, which are language- , genre-, and domain-independent and very effective, to infer the types of entity mentions. 
	- We design an unsupervised entity linking-based type naming approach to automatically generate fine-grained type labels, and jointly optimize clustering and linking.
	
Authors learn three representations:

**General Entity Representation: **

	- obtained by extracting the word embedding (word2vec) of the words of the mention, 
	
if the mention is composed of multiple words 

		- vectors are summed OR 
		- words are concatenated before the word2vec training

**Specific-Context Representation**

	- Given an entity mention, we first select its related concepts. For each AMR (Abstract Meaning Representation) relation we generate a representation based on the general embeddings of these related concepts. If a related concept doesn’t exist in the vocabulary, we generate its embedding based on the additive model. If there are several argument concepts involved in a specific relation, we average their representations. We concatenate the vector representations of all selected relations into one single vector. Though we have carefully aggregated and selected the popular relation types, the representation of each entity mention is still sparse. To reduce the dimensions and generate a high quality embedding for the specific context, we utilize the sparse auto-encoder framework to learn more low-dimensional representations.
	
**Knowledge Representation**

	- Given an entity e, we first collect all properties and type labels p(e) from the domain-specific knowledge bases (KBs). We remove the universal labels from all entities and construct a weighted undirected graph G = (V, E), where V is the set of entities in all KBs and E is the set of edges
	  the existence of an edge eij = (ei, ej ) implies that two entities, ei and ej , share some common properties or type labels. The weight of the edge, w(ei, ej ), is calculated as: common_properties/max_properties. After constructing the knowledge graph, we apply the graph embedding framework proposed by to generate a knowledge representation for each entity
	  
Then they apply hierarchical clustering on the concatenation of the three representations and automatically generate a label (using KB information)

They compare on specific datasets

#paper 