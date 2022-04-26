Based on: [What does BERT look at? An Analysis of BERT’s Attention](https://aclanthology.org/W19-4828.pdf), [Revealing the dark secrets of BERT](https://arxiv.org/pdf/1908.08593.pdf), [Are Sixteen Heads Really Better than One?](https://arxiv.org/pdf/1905.10650.pdf), [Analyzing Multi-Head Self-Attention: Specialized Heads Do the Heavy Lifting, the Rest Can Be Pruned](https://aclanthology.org/P19-1580.pdf)

Self-attention seems to encode syntactic relations 

There are different patters that can be observed by studying Self-attention with an attention matrix:
- Vertical: all attention values are activate on one token
- Diagonal: A diagonal can be seen on the attention matrix, basically attention is on previous and/or next word
- Vertical + Diagonal
- Block: Attentions values are clearly divided in two blocks following the \[SEP\] index in the input sentence
- Heterogeneous: Attention values are heterogenerously distributed, it is an interesting indicator for non-trivial relationships in the input text (said in the *[[Bertology Video]]*)

In [[Revealing the dark secrets of BERT|this paper]] is explained why the different patterns observed in self-attention matrix are not related with tasks and so not linguistically informative (based on the patterns counted on the GLUE tasks)

A finding of [[Revealing the dark secrets of BERT|this paper]] is that if attentions which have to exploit *important relations* (for example the attention value from a pronouns to the verb in a sentence) are zeroed out, there is no performance drop


