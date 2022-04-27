https://aclanthology.org/D18-1231.pdf

*Given a type taxonomy defined as Boolean functions of FREEBASE “types”, we ground a given mention to a set of type-compatible Wikipedia entries and then infer the target mention’s types using an inference algorithm that makes use of the types of these entries*

An approach towards [[Zero Shot Fine Grained Entity Typing]]

#### Introduction

In this work, we introduce ZOE, a zero-shot entity typing system, with open type definitions. Given a mention in a sentence and a taxonomy of entity types with their definitions, ZOE identifies a set of types that are appropriate for the mention in this context. ZOE does not require any training, and it makes use of existing data resources (e.g., Wikipedia) and tools developed without any task-specific annotation. The key idea is to ground each mention to a set of type-compatible Wikipedia entities. The benefit of using a set of Wikipedia titles as an intermediate representation for a mention is that there is much human-curated information in Wikipedia – categories associated with each page, FREEBASE types, and DBpedia types. These were put there independently of the task at hand and can be harnessed for many tasks: in particular, for determining the semantic types of a given mention in its context. In this grounding step, the guiding principle is that type-compatible entities often appear in similar contexts. We rely on contextual signals and, when available, surface forms, to rank Wikipedia titles and choose those that are more compatible with a given mention. 

Importantly, **our algorithm does not require a given mention to be in Wikipedia; in fact, in many cases (such as nominal mentions) the mentions are not available in Wikipedia. We hypothesize that any entity possible in English corresponds to some type-compatible entities in Wikipedia.** We can then rely mostly on the context to reveal a set of compatible titles, those that are likely to share semantic types with the target mention. The fact that our system is not required to ground to the exact concept is a key difference between our grounding and “standard” Wikification approaches (Mihalcea and Csomai, 2007; Ratinov et al., 2011). As a consequence, while entity linking approaches rely heavily on priors associated with the surface forms and do not consider those that do not link to Wikipedia titles, our system mostly relies on context, regardless of whether the grounding actually exists or not

#### Zero-Shot Open Entity Typing

Types are conceptual containers that bind entities together to form a coherent group. Among the entities of the same type, type-compatibility creates a network of loosely connected entities:

**Definition 1 (Weak Type Compatibility)** Two entities are type-compatible if they share at least one type with respect to a type taxonomy and the contexts in which they appear.

In our approach, given a mention in a sentence, we aim to discover type-compatible entities in Wikipedia and then infer the mention’s types using all the type-compatible entities together. The advantage of using Wikipedia entries is that the rich information associated with them allows us to infer the types more easily. Note that this problem is different from the standard entity linking or Wikification problem in which the goal is to find the corresponding entity in Wikipedia. Wikipedia does not contain all entities in the world, but an entity is likely to have at least one type-compatible entity in Wikipedia.

In order to find the type-compatible entities, we use the context of mentions as a proxy. Defining it formally:

**Definition 2 (Context Consistency)** A mention $m$ (in a context sentence $s$) is context-consistent with another well-defined mention $m_0$ , if $m$ can be replaced by $m_0$ in the context $s$, and the new sentence still makes logical sense.

**Hypothesis 1** Context consistency is a strong proxy for type compatibility

Based on this hypothesis, given a mention m in a sentence s, we find other context-compatible mentions in a Wikified corpus. Since the mentions in the Wikified corpus are linked to the corresponding Wikipedia entries, we can infer m’s types by aggregating information associated with these Wikipedia entries.

![[2018_zhou_architecture.png]]

The figure shows the high-level architecture of our proposed system. The inputs to the system are a mention $m$ in a sentence $s$, and a type definition $T$. The output of the system is a set of types $\{t_{Target}\} \subseteq T$ in the target taxonomy that best represents the given mention. The type definitions characterize the target entity-type space. In our experiments, we choose to use FREEBASE types to define the types across 7 datasets; that is, $T$ is a mapping from the set of FREEBASE types to the set of target types: $T : \{t_{FB}\} \rightarrow \{t_{Target}\}$. This definition comprises many atomic definitions; for example, we can define the type `location` as the disjunction of FREEBASE types like `FB.location` and `FB.geography`
![[2018_zhou_type_definition.png]]

The type definitions of a dataset reflect the understanding of a domain expert and the assumptions made in dataset design. Such definitions are often much cheaper to define, than to annotate full-fledged supervised datasets. It is important to emphasize that, to use our system on different datasets, one does not need to retrain it; there is one single system used across different datasets, working with different type definitions.

#### Experiments

Experiments are conducted on [[Dataset - Ren's BBN]], [[Dataset - Ren's FIGER]], [[Dataset - Ren's Ontonotes]], [[Dataset - MUC 7]], [[2003 Sang - Introduction to the CoNLL-2003 Shared Task, Language-Independent Named Entity Recognition]] and [[Dataset - OntoNotes v1]]



---

Ben Zhou 1 , 
Daniel Khashabi 2 , 
Chen-Tse Tsai 3 , 
Dan Roth 2

1 University of Illinois, Urbana-Champaign, 
2 University of Pennsylvania, 
3 Bloomberg LP

#paper 