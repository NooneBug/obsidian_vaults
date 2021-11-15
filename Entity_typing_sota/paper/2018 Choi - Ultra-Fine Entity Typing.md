https://arxiv.org/pdf/1807.04905.pdf

*We introduce a new entity typing task: given a sentence with an entity mention, the goal is to predict a set of free-form phrases (e.g. skyscraper, songwriter, or criminal) that describe appropriate types for the target entity. This formulation allows us to use a new type of distant supervision at large scale: head words, which indicate the type of the noun phrases they appear in. We show that these ultra-fine types can be crowd-sourced, and introduce new evaluation sets that are much more diverse and fine-grained than existing benchmarks. We present a model that can predict open types, and is trained using a multitask objective that pools our new head-word supervision with prior supervision from entity linking*

Defines Ultra Fine Entity Typing task, introduces a new dataset: [[Dataset - UFET]]

Authors propose also a model to perform Entity Typing task (and of course Ultra Fine Entity Typing) 

The model starts from [[2017 Shimaoka - Neural Architectures for Fine-grained Entity Type Classification]] so :
- uses GloVe [[Encoders - Pretrained Word Embeddings]]
- context representation is obtained by feeding the entire sentence into a LSTM, each word is represented with the GloVe word vector and a positional encoding that indicates if the word is on the left, inside, or on the right w.r.t. the mention [[Encoders - Neural Based Models - Recurrent architectures]], [[Encoders - Neural Based Models - Attention based architectures]]
- mention representation is obtained as a concatenation of:
	- a char-CNN on the entire mention span [[Encoders - Convolutional Networks]]
	- attention-weighted sum of GloVe word vectors

This approach uses [[Inference Method - Threshold or Max]] 

As a loss function, they simply divide the logistic regression loss into three losses, one fr each abstraction level of types. Given an abstraction level, its weights are updated only if a positive type of that abstraction level is in the groundtruth

The approach is evaluated on [[Dataset - Ren's Ontonotes]] and [[Dataset - UFET]]

#paper 