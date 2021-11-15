First datasets for Ultra Fine Entity Typing, introduced by [[2018 Choi - Ultra-Fine Entity Typing]]

First 6000 sentences are annotated with crowdsource, from GigaWord, Ontonotes and web articles, annotations are pair-agreed and each type is accepted only if at least 3/5 annotators agree

To select mentions a constituency parser and a coreference resolution system is used (this is probably the motivation behind the fact that only this datasets has pronouns as mentions), the dataset provides a well-rounded benchmark with roughly 40% pronouns, 38% nominal expressions, and 22% named entity mentions. The case of pronouns is particularly interesting, since the mention itself provides little information.

[[Distant Supervision]] is used to obtain a larger set of examples, using the manual 6000 sentences as input for the process:

	- To improve both entity and type coverage of KB supervision, we use definitions from Wikipedia. We follow Shnarch et al. who observed that the first sentence of a Wikipedia article often states the entity’s type via an “is a” relation; for example, “Roger Federer is a Swiss professional tennis player.” Since we are using a large type vocabulary, we can now mine this typing information.3 We extracted descriptions for 3.1M entities which contain 4,600 unique type labels such as “competition,” “movement,” and “village.”
	- Head words are extracted using a dependency parser and used as types

The type vocabulary is composed of >10k types, types can be partitioned in: 

	- 9 general types: person, location, object, organization, place, entity, object, time, event
	- 121 fine-grained types, mapped to fine-grained entity labels from prior work [[Dataset - FIGER]], [[Dataset - Ontonotes v5 - GFT]]
	- 10,201 ultra-fine types, encompassing every other label in the type space (e.g. detective, lawsuit, temple, weapon, composer)
	
On average, each example has 5 labels: 0.9 general, 0.6 fine-grained, and 3.9 ultra-fine types. Among the 10,000 ultra-fine types, 2,300 unique types were actually found in the 6,000 crowdsourced examples.

The crowdsourced dataset (Section 2.1) was randomly split into train, development, and test sets, each with about 2,000 examples. We use this relatively small manuallyannotated training set (Crowd in Table 4) alongside the two distant supervision sources: entity linking (KB and Wikipedia definitions) and head words. To combine supervision sources of different magnitudes (2K crowdsourced data, 4.7M entity linking data, and 20M head words), we sample a batch of equal size from each source at each iteration

Evaluation data has over 2,500 unique types, annotated with crowdsourcing, posing a challenging learning problem

#dataset 