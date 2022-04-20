https://www.ijcai.org/Proceedings/15/Papers/179.pdf

Introduce a #encoders_with_recurrent_architecture  to predict types for entity mentions. The model is based on the automatically learned distributed representations of mentions and contexts.

Introduce the [[Encoders - Sentence splitting]] 

Encodes the sentence in this way:

	- Mention tokens are fed into a RNN obtaining M
	- contexts tokens are treated separately but in the same way:
		- concatenation of the word vectors
		- hidden layer (obtaining L, R)
	- L M R are concatenated and fed in a classification layer (with softmax)

Word vectors are learned runtime, mention and context have separate word vectors, so in total there are 2 x Vocabulary vectors for words (two for each words, one for context and one for mention)

Authors propose [[Dataset - Wiki22]]

Experiments are conduced on [[Dataset - FIGER]] [[Dataset - YAGO505]] and [[Dataset - Wiki22]] (results reported on FIGER are in contrast with the original paper, so are not recorded in this obsidian vault)

Since softmax is used, probably produces [[Predictions - Single Path Prediction]] and [[Predictions - Partial Path Prediction]]

#paper #encoders_with_recurrent_architecture