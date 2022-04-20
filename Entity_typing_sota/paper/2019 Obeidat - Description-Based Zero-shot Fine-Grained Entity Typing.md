https://aclanthology.org/N19-1087.pdf

*This work proposes a zero-shot entity typing approach that utilizes the type description available from Wikipedia to build a distributed semantic representation of the types. During training, our system learns to align the entity mentions and their corresponding type representations on the known types. At test time, any new type can be incorporated into the system given its Wikipedia descriptions*

[[Zero Shot Fine Grained Entity Typing]]

*We learn to project the entity-mention representations and the type representations into a shared semantic space, such that the mention is closer to the correct type(s) than the incorrect types. The mid-level type representation derived from the Wikipedia page along with the learned projection function allows the system to recognize new types requiring zero training examples*

*Note that the descriptions can be quite long, often containing many different parts that are useful for recognizing different entity mentions. This motivates us to generate a bag of representations for each type and apply average pooling to aggregate the results.*

*
• We proposed a description-based zero-shot fine-grained entity typing framework that uses Wikipedia descriptions to represent and detect novel types unseen in training. 
• We created a new test set for fine-grained entity typing that provides much better coverage of the level-2 (fine-grained) types compared to the original FIGER test data. 
• We provided experimental evidence of the effectiveness of our approach in comparison with established baselines*

The type representation [[Models with Type Representations]] and the input representation are represented in the same joint space and compared with dot product

- The entity mention representation is obtained with the same approach as [[2017 Shimaoka - Neural Architectures for Fine-grained Entity Type Classification]] #encoders_with_recurrent_architecture #pretrained_word_embeddings_glove 
- Type representation is obtained by averaging wikipedia definitions of the type
	- Since definition are long, they are divided in paragraph and different bag of word representation are obtained (average of the vectors of each word in the paragraph)
	- Then a score for each representation is computed and the average of the score is used to perform the inference

Experiments are conduced on [[Dataset - Ren's FIGER]]

#paper #encoders_with_recurrent_architecture #pretrained_word_embeddings_glove 