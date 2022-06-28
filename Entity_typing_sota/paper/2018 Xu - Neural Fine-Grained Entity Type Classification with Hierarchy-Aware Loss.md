https://arxiv.org/pdf/1803.03378.pdf

https://github.com/billy-inn/NFETC

First paper that explicitly talking about [[Noise Definition - Out-of-context]] and [[Noise Definition - Overly Specific]]

#### Abstract

We propose an end-to-end solution with a neural network model that uses a variant of cross-entropy loss function to handle out-of-context labels, and hierarchical loss normalization to cope with overly-specific ones. Also, previous work solve FETC a multi-label classification followed by ad-hoc post-processing. In contrast, our solution is more elegant: we use public word embeddings to train a single-label that jointly learns representations for entity mentions and their context. We show experimentally that our approach is robust against noise and consistently outperforms the state-of-theart on established benchmarks for the task.

#### Introduction

![[2018_xu_idea.png]]

One kind of noise introduced by distant supervision is assigning labels that are out-of-context (athlete in S1 and coach in S2) for the sentence. Current FETC systems sidestep the issue by either ignoring out-of-context labels or using simple pruning heuristics like discarding training examples with entities assigned to multiple types in the knowledge graph. However, both strategies are inelegant and hurt accuracy.

Another source of noise introduced by distant supervision is when the type is overly-specific for the context. For instance, example S3 does not support the inference that Mr. Kerr is either an athlete or a coach. Since existing knowledge graphs give more attention to notable entities with more specific types, overly-specific labels bias the model towards popular subtypes instead of generic ones, i.e., preferring athlete over person. Instead of correcting for this bias, most existing FETC systems ignore the problem and treat each type equally and independently, ignoring that many types are semantically related.

Besides failing to handle noisy training data there are two other limitations of previous FETC approaches we seek to address. First, they rely on hand-crafted features derived from various NLP tools; therefore, the inevitable errors introduced by these tools propagate to the FETC systems via the training data. Second, previous systems treat FETC as a multi-label classification problem: during type inference they predict a plausibility score for each type, and, then, either classify types with scores above a threshold (Mintz et al., 2009; Gillick et al., 2014; Shimaoka et al., 2017) or perform a top-down search in the given type hierarchy (Ren et al., 2016a; Abhishek et al., 2017).

**Contributions:** We propose a neural network based model to overcome the drawbacks of existing FETC systems mentioned above. With publicly available word embeddings as input, we learn two different entity representations and use bidirectional long-short term memory (LSTM) with attention to learn the context representation. We propose a variant of cross entropy loss function to handle out-of-context labels automatically during the training phase. Also, **we introduce hierarchical loss normalization to adjust the penalties for correlated types, allowing our model to understand the type hierarchy and alleviate the negative effect of overly-specific labels**.

tl:dr: Authors use [[Noise Definition - SIngle Path vs Multi-Path]], assuming that only single path types are to predict and so [[Dataset Modification - 2018 Xu - Multilabel to single label |casting the multilabel entity typing task in a single label task]], using the terminal node for each possible single-path and inferring the ancestors after.
	*Moreover, in order to simplify the problem and take advantage of previous research on hierarchical classification, we transform the multi-label classification problem to a single-label classification problem. Based on the assumption that each mention can only have one type-path depending on the context, we leverage the fact that type hierarchies are forests, and represent each type-path uniquely by the terminal type (which might not be a leaf node). For Example, type-path root-person-coach can be represented as just coach, while root-person can be unambiguously represented as the non-leaf person.*

#### Background and Problem

We represent the training corpus using a set of mention-based triples $D = {(m_i , c_i , Y_i)}^N_{i=1}$. If $Y_i$ is free of out-of-context noise, the type labels for each $m_i$ should form a single type-path in $Y_i$ . However, $Y_i$ may contain type-paths that are irrelevant to $m_i$ in $c_i$ if there exists out-of-context noise.

We denote the type set including all terminal types for each type-path as the target type set $Y^t_i$ . In the example type hierarchy shown in Figure 1, if $Y_i$ contains types `person`, `athlete`, `coach`, $Y^t_i$ should contain `athlete`, `coach`, but not `person`. In order to understand the trade-off between the effect of out-of-context noise and the size of the training set, we report on experiments with two different training sets: $D_{filtered}$ only with triples whose $Y_i$ form a single type-path in $D_i$, and $D_{raw}$ with all triples.

We formulate fine-grained entity classification problem as follows: 

**Definition 1** Given an entity mention $m_i = (w_p, . . . , w_t) (p, t \in [1, T], p \leq t)$ and its context ci = (w1, . . . , wT ) where $T$ is the context length, our task is to predict its most specific type $y^i$ depending on the context. 
In practice, $c_i$ is generated by truncating the original context with words beyond the context window size $C$ both to the left and to the right of $m_i$ . Specifically, we compute a probability distribution over all the $K = |Y|$ types in the target type hierarchy $Y$. The type with the highest probability is classified as the predicted type $y^i$ which is the terminal type of the predicted type-path.

#### Methodology
![[2018_xu_architecture.png]]

The encoder is [[Xu Encoder]]

We concatenate context representation and two mention representations together to form the overall feature representation of the input $R = [r_c, r_a, r_l ]$. Then we use a softmax classifier to predict $y^i$ from a discrete set of classes for a entity mention $m$ and its context $c$ with $R$ as input: $\hat p(y|m,c) = softmax(WR + b)$ and $\hat y = argmax_y \hat p(y|m, c)$ where $W$ can be treated as the learned type embeddings and b is the bias.


Authors propose two different losses:

- A simple modification of the BCE to apply on Multi-Path examples: in this case, if the type with the max probability is one of the multi-path types, then is considered correct

**Hierarchical Loss Normalization**

tl:dr, for each type, the final probability is obtained by summing the type probability to the weighted sum of probabilities of the ancestors.  

Since the fine-grained types tend to form a forest of type hierarchies, it is unreasonable to treat every type equally. Intuitively, it is better to predict an ancestor type of the true type than some other unrelated type. For instance, if one example is labeled as `athlete`, it is reasonable to predict its type as `person`. However, predicting other high level types like `location` or `organization` would be inappropriate. In other words, we want the loss function to penalize less the cases where types are related. Based on the above idea, we adjust the estimated probability as follows: $p^*(\hat y|m, c) = p(\hat y|m, c) + \beta * \sum_{t \in \tau}p(t| m, c)$  where $\tau$ is the set of ancestor types along the type-path of $\hat y$, $\beta$ is a hyperparameter to tune the penalty. Afterwards, we re-normalize it back to a probability distribution, a process which we denote as hierarchical loss normalization.

As discussed in Section 1, there exists overly-specific noise in the automatically labeled training sets which hurt the model performance severely. With hierarchical loss normalization, the model will get less penalty when it predicts the actual type for one example with overly-specific noise. Hence, it can alleviate the negative effect of overly-specific noise effectively. Generally, hierarchical loss normalization can make the model somewhat understand the given type hierarchy and learn to detect those overly-specific cases. During classification, it will make the models prefer generic types unless there is a strong indicator for a more specific type in the context.

#### Experiment

This approach is experimented on [[Dataset - Ren's Ontonotes]] and [[Dataset - Ren's FIGER]]

We run each model with the welltuned hyperparameter setting five times and report their average strict accuracy, macro F1 and micro F1 on the test set. The proposed model was implemented using the TensorFlow framework.

**Discussion about Out-of-context Noise** 

For dataset FIGER, the performance of our model with the proposed variant of cross-entropy loss trained on $D_{raw}$ is significantly better than the basic neural model trained on $D_{filtered}$, suggesting that the proposed variant of the cross-entropy loss function can make use of the data with out-of-context noise effectively. On the other hand, the improvement introduced by our proposed variant of cross-entropy loss is not as significant for the OntoNotes benchmark. This may be caused by the fact that OntoNotes is much smaller than FIGER(GOLD) and proportion of examples without out-of-context noise are also higher.

**Investigations on Overly-Specific Noise** 
With hierarchical loss normalization, the performance of our models are consistently better no matter whether trained on $D_{raw}$ or $D_{filtered}$ on both datasets, demonstrating the effectiveness of this hierarchical loss normalization and showing that overly-specific noise has a potentially significant influence on the performance of FETC systems.

---
# Old
"Existing methods rely on distant supervision and are thus susceptible to noisy labels that can be out-of-context or overly-specific for the training sentence. Previous methods that attempt to address these issues do so with heuristics or with the help of hand-crafted features. Instead, we propose an end-to-end solution with a neural network model that uses a variant of crossentropy loss function to handle out-of-context labels, and hierarchical loss normalization to cope with overly-specific ones. Also, previous work solve FETC a multi-label classification followed by ad-hoc post-processing. In contrast, our solution is more elegant: we use public word embeddings to train a single-label that jointly learns representations for entity mentions and their context."

First paper that explicitly talking about [[Noise Definition - Out-of-context]] and [[Noise Definition - Overly Specific]]

Authors use [[Noise Definition - SIngle Path vs Multi-Path]], assuming that only single path types are to predict and so [[Dataset Modification - 2018 Xu - Multilabel to single label |casting the multilabel entity typing task in a single label task]], using the terminal node for each possible single-path and inferring the ancestors after.


Authors propose two different losses:

- A simple modification of the BCE to apply on Multi-Path examples: in this case, if the type with the max probability is one of the multi-path types, then is considered correct
- A hierarchy-aware loss: the probability of each type is raised by a fraction of the probability of all its ancestors (i.e. athlete has a probability composed by the one of athlete itself and a bit of the one of person)

This approach is experimented on [[Dataset - Ren's Ontonotes]] and [[Dataset - Ren's FIGER]]

#paper #encoder_with_attention #encoders_with_recurrent_architecture