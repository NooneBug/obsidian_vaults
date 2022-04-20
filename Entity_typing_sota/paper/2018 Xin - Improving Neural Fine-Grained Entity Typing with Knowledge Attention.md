http://nlp.csai.tsinghua.edu.cn/~lyk/publications/aaai2018_entitytyping.pdf

*we take information from KBs into consideration to bridge entity mentions and their context together, and thereby propose Knowledge-Attention Neural Fine-Grained Entity Typing.*

*we propose KnowledgeAttention Neural Fine-Grained Entity Typing (KNET). Our model mainly consists of two parts. Firstly, we build a neural network to generate context and entity mention representations. Secondly, depending on the entity mention, we use knowledge attention to focus on important context words and improve the quality of context representation. Knowledge attention is computed using entity embeddings, which are learned from KB relational information and reconstructed from the text. Considering we will encounter both in-KB and out-of-KB entities in testing, we propose a disambiguation procedure, which can provide not only in-KB entities with precise KB information, but also out-of-KB entities with useful knowledge. *

![[2018_xin_architeture.png]]

They propose a recurrent neural network to encode the input sentence and the and a neural network to encode entity information from a KB. #encoders_with_recurrent_architecture , #encoder_with_attention , #pretrained_word_embeddings_glove 

The sentence encoder is composed of three components:

	- the entity mention representation is composed by averaging the word vectors of which the mention is composed
	- an KB entity encoder (TransE) 
	- the context representations are obtained by applying an LSTM (different from left and right context).

This approach also used three different definition of attention:

	- The one from 2017 Shimaoka
	- An attention approach applied only on mention representation
	- An attention approach applied on a KB mention representation (the one in the image)

The authors also provide a disambiguation mechanism in order to decide which KB mention representation use.

The authors propose two datasets: WIKI-MAN and WIKI-AUTO that contains also explicit information to link entities in a KB 

#paper #encoder_with_attention #encoders_with_recurrent_architecture #pretrained_word_embeddings_glove 