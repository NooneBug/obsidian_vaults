https://aclanthology.org/D19-1641.pdf

*We propose a fine-grained entity typing model with a novel attention mechanism and a hybrid type classifier. We advance existing methods in two aspects: feature extraction and type prediction. To capture richer contextual information, we adopt contextualized word representations instead of fixed word embeddings used in previous work. In addition, we propose a two-step mention-aware attention mechanism to enable the model to focus on important words in mentions and contexts. We also present a hybrid classification method beyond binary relevance to exploit type interdependency with latent type representation. Instead of independently predicting each type, we predict a low-dimensional vector that encodes latent type features and reconstruct the type vector from this latent representation.*

![[2019_lin_architecture.png]]

The architecture is composed of these modules: 

- Sentence Encoder: [[Encoders - Neural Based Models - ELMo based architectures]]
- Mention Encoder: Weighted sum of ELMo Representation, weights learned with attention #encoder_with_attention 
- Context Encoder: weighted sum of ELMo Representation, weights learned with attention #encoder_with_attention 

For the inference, this approach has [[Models with Type Representations]] learned runtime, but also use these embedding to generate a type representation with few dimensions, obtained by LSA; in this way will combine representation dependent from the input with underlying type correlation 

In this way two representations for each type are learned, and two projection function from the input representation to the two spaces are learned

Once logits for each type are obtained [[Inference Method - Threshold or Max]] is   used

The approach is evaluated on [[Dataset - Ren's Ontonotes]], [[Dataset - FIGER]], [[Dataset - Ren's BBN]] and datasets from 2018 Xin

#paper #encoder_with_attention 