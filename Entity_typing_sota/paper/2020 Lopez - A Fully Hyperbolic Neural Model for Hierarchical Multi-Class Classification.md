https://arxiv.org/pdf/2010.02053.pdf

*"This is the first work that proposes a fully hyperbolic model for multi-class multi-label classification, which performs all operations in hyperbolic space"*

*"Our hyperbolic model infers the latent hierarchy from the class distribution, captures implicit hyponymic relations in the inventory, and shows performance on par with state-ofthe-art methods on fine-grained classification with remarkable reduction of the parameter size"*

The model architecture is composed as: 

![[2020_Lopez_Architecture.png]]

-	Mention Encoder #pretrained_word_embeddings_glove, #encoders_with_recurrent_architecture :
	-	Weighted sum of Hyperbolic Word Embeddings for each word of the mention
	-	Hyperbolic RNN over Hyperbolic Word Embeddings
-	Context Encoder #encoders_with_recurrent_architecture : 
	-	GRU over Hyperbolic Word Embeddings

Then hyperbolic attention is applied #encoder_with_attention 

The prediction is performed through an hyperbolic multinomial logistic regression, after applying the sigmoid each type with threhsold >.5 is taken [[Predictions - Multiple Path Precition]], [[Predictions - Partial Path Prediction]]

The approach is evaluated on [[Dataset - UFET]] and [[Dataset - Ren's Ontonotes]]

#paper #encoder_with_attention #encoders_with_recurrent_architecture #pretrained_word_embeddings_glove 