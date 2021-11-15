https://aclanthology.org/P18-1010.pdf

"This paper presents new methods using real and complex bilinear mappings for integrating hierarchical information, yielding substantial improvement over flat predictions in entity linking and fine-grained entity typing, and achieving new state-of-the-art results for end-to-end models on the benchmark FIGER dataset."

Authors provide two new [[Ultra Fine Entity Typing]] datasets: MedMentions and TypeNet (which are Now (Nov 2021) are not used outside this work and so are not described)

The sentence encoder is based on [[Encoders - Pretrained Word Embeddings]], [[Encoders - Convolutional Networks]] and [[Encoders - Neural Based Models]]

	- Mention is encoded by averaging word vectors
	- Context is encoded togheter with mention using Word Level CNN with maxpool with window = 5
	- Word vectors are concatenated with positional information (Each token within the distinguished mention span has position 0, tokens to the left have a negative distance from [−s, 0), and tokens to the right of the mention span have a positive distance from (0, s].)

This approach is based on a [[Models with Type Representations]]. Type vectors are generated using RESCAL or ComplEx

The approach is experimented on [[Dataset - Ren's FIGER]], MedMentions and TypeNet



#paper 