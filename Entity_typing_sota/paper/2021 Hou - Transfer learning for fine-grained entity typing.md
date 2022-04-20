https://link.springer.com/content/pdf/10.1007/s10115-021-01549-5.pdf

*"In this paper, we propose a transfer learning-based approach to extract more efficient feature representations and offset label noises. More precisely, we adopt three transfer learning schemes: 
	(i) transferring sub-word embeddings to generate more efficient OOV 	embeddings; 
	(ii) using a pre-trained language model to generate more efficient context features; 
	(iii) using a pre-trained topic model to transfer the topic-type relatedness    through topic anchors and select confusing fine-grained types at inference time. The pre-trained topic model can offset the label noises without retreating to coarse-grained types."*
	
---
***Contribution: ***
	
"*
- We introduce a novel transfer learning architecture that combines a non-recurrent neural language model and a topic model. Our transfer learning architecture is different from the recent transfer learning methods being used in NLP tasks that mainly focus on language models. The intuition behind is that the language model is able to capture the local context, while the topic model is able to find the distributions of words and semantic classes across documents and latent topics.
- We show that the topic model is capable of transferring the learned associations between semantic types and hidden topics. The document level topic label has been used as a feature for FGET  or used to reduce label noises. But their topics are obtained through a supervised text classification model. However, in the new approach, we use the learned topic model to guide the inference of a typing model instead. Such mechanism can reduce the confusion caused by label noises without retreating to coarse grained types.
- We use transfer learning to generate the embedding vectors of out-of-vocabulary (OOV) words that are constituents of entity mentions. Previous work on FGET learned the embedding vectors of OOVs during the training of the FGET classifier. This leads to insufficient training, and the sub-word level information of OOVs is ignored. We use the sub-word level patterns to estimate the embeddings of OOVs based on embeddings of character n-grams.
- We use a pre-trained language model to encode context features. Most of the previous work used LSTM trained on FGET data set with label noises. This makes the LSTM network incompetent at encoding effective context features. The deep neural language model pre-trained on clean corpus can generate more efficient feature representations.
*"

[[2021 Hou Literature References | This article depicts well the Fine-Grained Entity Typing literature]]  

This article propose Transfer Learning for fine-grained entity typing in sense of use pretrained models to add information in the FGET task. The used pretrained models are:

- Language Models: [[Encoders - Neural Based Models - BERT Based Architectures | SpanBERT]]
- Topic Models: HMM-LDA
- Vector Representation of words: #pretrained_word_embeddings_fasttext, LSTM #encoders_with_recurrent_architecture 

*"We formulate the typing model for FGET as a local binary classifier on each type of the taxonomy. The typing model makes predictions based on the feature representations of mention phrase and context. For each mention $m$, we denote the embedded mention feature as $v_m$ and the context feature as $v_c$. The probability of entity mention $m$ being type $t_i$ can be computed by: $P(t_i | m, c) = \sigma(f_i(concat(v_m, v_c) + b)$"*

This approach uses also denoising: "*We train our typing classifier on intact noisy corpus. Then, we select multiple labels based on the probability and filter out those irrelevant labels using topic-type relatedness*"

Authors use LDA to model the topics
 
 ![[2021_hou_architecture.png]]
 
 The proposed architecture is composed as:
 
 - The input encoder is a combinarion of FastText, LSTM, SpanBERT and topic model
 - the classifier is simple a binary classifier for each type, trained with BCE
 
 The inference method is quite complex:
 
 - To improve the recall of types, we use a relatively small threshold. We then employ the following inference strategy to assign type labels: 
	 - (i) If there are neither level 2 nor level 3 fine-grained types, then select the level 1 coarse grained type with highest probability. 
	 - (ii) If there is only one level 2 type, then select the types on the label path.
	 - (iii) If there are multiple level 2 types, then use pre-trained topic model to filter out irrelevant types

The approach is evaluated on [[Dataset - Ren's FIGER]], [[Dataset - Ren's Ontonotes]]
 
---

Feng Hou · Ruili Wang · Yi Zhou 

School of Natural and Computational Sciences, Massey University, Albany, New Zealand (1, 2)

Shanghai Research Center for Brain Science and Brain-Inspired Intelligence, Zhangjiang Lab, Shanghai, China (3)

#paper #encoders_with_recurrent_architecture #pretrained_word_embeddings_fasttext 