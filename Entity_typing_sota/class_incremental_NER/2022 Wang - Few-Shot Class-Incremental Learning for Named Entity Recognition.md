https://aclanthology.org/2022.acl-long.43.pdf

Previous work of class-incremental learning for Named Entity Recognition (NER) relies on the assumption that there exists abundance of labeled data for the training of new classes. In this work, we study a more challenging but practical problem, i.e., few-shot classincremental learning for NER, where an NER model is trained with only few labeled samples of the new classes, without forgetting knowledge of the old ones. To alleviate the problem of catastrophic forgetting in few-shot classincremental learning, we generate synthetic data of the old classes using the trained NER model, augmenting the training of new classes. We further develop a framework that distills from the NER model from previous steps with both synthetic data, and real data from the current training set.

In practice, data of new entity classes that the NER model has not seen during training arrives constantly, thus it is desirable that the NER model can be incrementally updated over time with knowledge of data for these new classes. In this case, one challenge is that the training data of old entity classes may not be available due to privacy concerns or memory limitations [[2020 Ma - Adversarial Self-Supervised Data-Free Distillation for Text Classification|2020 Ma]].

In addressing this problem, previous work in class-incremental learning for NER (Monaikul et al., 2021) regularizes the current model by distilling from the previous model trained on old (existing) classes, using text from the training dataset of new classes. However, this requires abundance of data in the new training dataset being used for distillation. Such an assumption is usually unrealistic since the token-level annotations required by NER training are labor-consuming and scarce, especially for the new unseen classes.

In this paper, we study a more realistic setting, i.e., few-shot classincremental learning for NER, where the model (i) incrementally learns on new classes with few annotations, and (ii) without requiring access to training data for old classes.

There is very limited work in few-shot class-incremental learning for NER. Such a setting is more challenging compared with class-incremental learning for NER. First, the few-shot datasets in few-shot class-incremental learning may not contain enough information for the trained model to generalize during testing. Second, it is more challenging to solve the catastrophic forgetting problem in few-shot class-incremental learning when data for old classes is not available and new data is scarce. In class-incremental learning for NER (Monaikul et al., 2021), the same training sequence may contain entities of different classes. Therefore, when the training dataset for new classes is sufficiently large, its context, i.e., words labeled as not from entities of new classes, may also contain abundant entities of the old classes.
That is, the new training data can be regarded as an unlabeled replay dataset of the existing entity classes. In such case, we can simply address the problem of catastrophic forgetting by distilling from the previous model (trained on old classes) to the current one, using text from such a replay dataset (Monaikul et al., 2021). However, in few-shot classincremental learning, we cannot expect to avoid catastrophic forgetting by distilling with only the few samples from the new training dataset, since there may not exist sufficient (if any) entities of the old classes.

In this paper, we propose a framework to enable few-shot class-incremental learning for NER. As mentioned above, since the few-shot dataset may not contain enough entities of old classes as replay data for distilling from the previous model, which leads to catastrophic forgetting, we consider generating synthetic data of the old entity classes for distillation. Such data is termed as synthetic replay. Specifically, we generate synthetic data samples of old classes by inverting the NER model. Given the previous model trained on the old classes, we optimize the token embeddings of the synthetic data, so that predictions from the previous model can contain old entity classes, given the synthetic data as input. In this way, the synthetic data is likely to contain entities of old classes, and distilling from the previous model with such data will thus encourage knowledge preservation of old classes. Additionally, to ensure the synthetic (reconstructed) data to be realistic, we propose to leverage the readily available real text data for new classes, via adversarially matching the hidden features of tokens from the synthetic data and those from the real data. Note that the synthetic data generated from such adversarial match with real data will contain semantics that are close to the real text data for new classes. Consequently, compared with training with only the few samples of new classes, the synthetic data will provide more diverse context that are close to the samples of the few-shot dataset, augmenting the few-shot training for the new classes.

Further, with the generated synthetic data, we propose a framework that trains the NER model with annotations of the new classes, while distilling from the previous model with both the synthetic data and real text from the new training data. Our contributions of this work are summarized as follows: 
- We present the first work of studying few-shot incremental learning for Named Entity Recognition (NER), a more practical but challenging problem compared with class-incremental learning for NER. 
- We approach the problem by proposing a framework that distills from the existing model with both, real data of new entity classes and synthetic data reconstructed from the model as replay data of old entity classes.
- Experiments show that our method significantly improves over existing baselines for the task of few-shot class-incremental learning in NER


We do not learn separate prediction modules for each time step.

The training is divided in different steps:

## Framework

Using BERT-CRF as NER classifier $M$, the author assume to have a model $M^{t-1}$ trained to recognize some types $D^{t-1}$ and train it on types $D^t$
obtaining $M^t$, note that $D^{t-1}$ and $D^{t}$ are disjoint.

### Distilling from Real Data $D^{t}$

$M^{t}$ is trained under distillation procedure to match the predictions of $M^{t-1}$ on the top predicted types for each input tokens, excluding the tokens annotated with types from $D^t$ that are unknown to $M^{t-1}$.

### Distilling from Synthetic Data $D^t_r$

On synthetic data, each predicted $O$ can possibly be an entity with type $\in D^T$. So the distillation procedure to match the predictions of $M^{t-1}$ aggregates predictions of $O$ and new types $\in D^T$ and only after this aggregation the distributions are optimized.

### Synthetic Data Reconstruction

To avoid forgetting on types $D^{t-1}$, on which there are not real annotated data on at time $t$, a synthetic dataset is generated: given a type sequence $Y$ composed of types $\in D^{T-1}$ the input tokens $X$ are optimized to obtain $Y$ from $M^{t-1}(X)$. To avoid the possibility of generating unrealistic text the representations on even BERT's layers ($2$, $4$, $...$, $12$) are optimized to be as similar as possible to correspective representations obtained from real sentences (from real data $D^t$)



#paper 