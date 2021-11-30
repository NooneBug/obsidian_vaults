https://www.ijcai.org/Proceedings/2019/0731.pdf

*In this paper, we directly model the structured, noisy labels with a novel content-sensitive weighting schema. Coupled with a newly devised cost function and a hierarchical type embedding strategy, our method leverages a random walk process to effectively weight out noisy labels during training.*

*To directly model the structured noisy labels for FET, in this paper, we propose a novel content-sensitive weighting schema that is powered by a newly devised cost function and a hierarchical type embedding strategy. In detail, the hierarchically structured typing labels in the given data are first normalized to having only the leaf nodes of the tree as candidate types. Next, context dependent weights for all typing labels are then randomly initialized. Finally, through maximizing the expected reward of a random walk process, the weights of all candidate types are re-weighted such that only one of them will have large value, which corresponds to the correct type. In this way, the proposed weighting schema is able to effectively denoise the noisy hierarchical typing labels during training, thus improving the predictive performance of the FET models*

![[2019_wu_idea.png]] ![[2019_wu_tree.png]]

*We denote our method as Noise Detective Prediction (NDP). In a nutshell, our NDP method first normalizes the hierarchically structured typing labels, so that only the leaf nodes represent valid type. Next, a loss constraint is used to regularize the training to weight out noisy labels.*

The approach is composed of these steps:

- Add a STOP node as son of each non-leaf node (figure 3), now each type can be identified by a leaf node. This approach allows [[Predictions - Partial Path Prediction]]
- Label is inferred with a complex graph based approach (see the paper)
- Type Embedding is computed as the sum of vectors each word in the name of the type and its ancestors. Using [[Encoders - Pretrained Word Embeddings]] (GloVe), [[Models with Type Representations]]
- Entity mention embedding is the average of the vectors of the words (GloVe)
- Context Embedding is a BiLSTM fed with GloVe vectors and attention [[Encoders - Neural Based Models - Recurrent architectures]], [[Encoders - Neural Based Models - Attention based architectures]]


Approach is evaluated on [[Dataset - Ren's BBN]], [[Dataset - Ren's FIGER]], [[Dataset - Ren's Ontonotes]]

#paper 