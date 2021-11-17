https://arxiv.org/pdf/1905.01566.pdf

*In this work, we propose a two-stage procedure for handling this type of data: denoise it with a learned model, then train our final model on clean and denoised distant data with standard supervised training. Our denoising approach consists of two parts. First, a filtering function discards examples from the distantly labeled data that are wholly unusable. Second, a relabeling function repairs noisy labels for the retained examples. Each of these components is a model trained on synthetically-noised examples generated from a small manually-labeled set.*

*Concretely, we implement our approach for the task of fine-grained entity typing, where a single entity may be assigned many labels. We learn two denoising functions: a relabeling function takes an entity mention with a noisy set of types and returns a cleaner set of types, closer to what manually labeled data has. A filtering function discards examples which are deemed too noisy to be useful. These functions are learned by taking manually labeled training data, synthetically adding noise to it, and learning to denoise, similar to a conditional variant of a denoising autoencoder (Vincent et al., 2008). Our denoising models embed both entities and labels to make their predictions, mirroring the structure of the final entity typing model itself*

This article proposes a denoising approach, obtaining a [[Denoising Techniques - Modify the training set]] and a typing approach to be trained on the obtained corpus 

[[Denoising Techniques - Onoe]]  

The typing network is composed as follows

![[2019_onoe_typing_network.png]]

The input encoder is composed of four modules:

- Sentence Representation : bi-LSTM over ELMo vectors
- Word level mention representation : Bi-LSTM over ELMo vectors
- Character level mention representation : char-CNN 
- Headword mention vector : ELMo vectors of the headword, extracted with spacy

The first three modules are the same as in [[2018 Choi - Ultra-Fine Entity Typing]] but with ELMo encodings instead of GloVe [[Encoders - Neural Based Models - ELMo based architectures]]

The decoder is simply a sigmoid over all classes, the inference function is [[Inference Method - Threshold or Max]]

The loss function is [[Losses - Choi Loss]]

Approach is experimented on [[Dataset - UFET]] and [[Dataset - Ren's Ontonotes]]

#paper 