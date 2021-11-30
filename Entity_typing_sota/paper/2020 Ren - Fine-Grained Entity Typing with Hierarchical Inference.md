https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9085112&tag=1

*Recent models do not explicitly consider the hierarchical structure of the type set in type inference. Some state-of-the-art models transform the problem from a multi-label classification to a single-label classification, which results in the confirmation bias. Therefore, we propose a neural model that can effectively capture entity information from the context and the mention aspects and hierarchical inference, which hierarchically infers types layer by layer in type set. In the optimization process, we also introduce a penalty term that can effectively alleviate the side effect of the confirmation bias and label noise introduced by distant supervision*

*To address limitations as mentioned above, we propose the Fine-Grained Entity Typing with Hierarchical Inference (FETHI), which automatically denoises the training data, and hierarchically infers entity type layer by layer. In the training process, we use word-level and character-level LSTM to learn features in different granularity. In the inferring process, human annotators usually perform a top-down inference when annotating an entity mention. For example, when judging whether an entity is a musician or director on the premise that we have assumed the entity is a person. Inspired by this behavior, our model first infers the type in a comparatively abstract concept, then infer the sub-type based explicitly on previous inference information(Figure 1).*

![[2020_ren_architettura.png]]

The architecture is composed as follows: 

-	Word-level representation: a sentence is represented though a [[Encoders - Neural Based Models - Recurrent architectures | Bi-LSTM]] with [[Encoders - Neural Based Models - Attention based architectures | self-attention]]. Mention is represented in a tricky way (*not really well explained*).
-	Char-level representation: char embedding of the mention characters.

Then the model [[Hierarchy Representation - 2020 Ren | represent the hierarchy internally]]

The loss is Binary Cross Entropy

They apply a [[Denoising Techniques - 2020 Ren | denoising technique]] under [[Noise Definition - Single Ancestor vs Multi Ancestor| their own noise definition]]

The inference is hierarchical and is the same as [[Inference Method - Hierarchical Inference - 2016 Ren | Ren, Abishek]] and so the [[Predictions - Single Path Prediction | predictions are strictly single path]] with an optimization on the threshold value

The approach is experimented on [[Dataset - Ren's FIGER]], [[Dataset - Ren's Ontonotes]]
 

#paper 