https://www.ijcai.org/Proceedings/2020/0527.pdf

*"In this paper, we propose a probabilistic automatic relabeling method which treats all training samples uniformly. Our method aims to estimate the pseudo-truth label distribution of each sample, and the pseudo-truth distribution will be treated as part of trainable parameters which are jointly updated during the training process. The proposed approach does not rely on any prerequisite or extra supervision, making it effective on real applications"*

*"Consequently, previous studies suffer from two limitations: 
	1) Still rely on some prerequisites (e.g. human-curated clean dataset), making them inefficient in real applications; 
	2) Incapable of eliminating the impact of samples with only one type label but are false positive (Table 4 shows more details)."*
	
![[2020_zhang_tab4.png]]

*"In this paper, to handle the above two limitations simultaneously, we propose a probabilistic automatic relabeling method. As the ground-truth label distribution is not available, our method aims at estimating the pseudo-truth label distribution during the training process. In detail, each sample is assigned a continuous label distribution $\tilde p$ over all candidate labels, and $\tilde p$ will be jointly updated as trainable parameters through the back-propagation algorithm."*

"*The learning  purpose is minimizing the Kullback-Leibler (KL) divergence between the predicted distribution and the pseudo-truth label distribution. Finally, **we take the label with the highest value in $\tilde p$ as the only one pseudo-truth label**. In order to ensure the rationality of the final estimated pseudo-truth distribution, we integrate the golden-noisy information during the training process with two specific designed constraints. In this way, our method can effectively relabel the noisy distant samples during training, thus improving the predictive performance."*

This approach is a #model_robust_to_noise 
and use the [[Dataset Modification - 2018 Xu - Multilabel to single label | Xu dataset modification (Multilabel to single label)]] *"The basic assumption of our idea is: for each mention-context pair (m, c), there exists only one most appropriate type given the candidate set T"*

The model is composed as follows:

![[2020_zhang_architecture.png]]

- Feature encoder: the same as [[Xu Encoder]]	

The prediction module is a quite complex:

First a single label prediction module is trained (single label is extracted through softmax and optimized with BCE)

The a **automatic relabeling module** is used: under the assumption that for each mention-context pair exists only one most appropriate type given the candidate set. Authors want to learn a pseudo-representation for each type and let the model to predict that representation (like [[Models with Type Representations]]); but they pose constraints on the learnt type representation (called pseudo-type distribution): 
	- each component $p_{ij}$ of the pseudo-type distribution has values only between $[0, 1]$ with $\sum_j p_{ij} = 1$
	- the pseudo-type distribution is learnt by optimizing KL-divergence between the pseudo-type distribution and the input representation (for each true type)
	- pseudo-type distribution is initialized with $softmax(y)$ (not clear how $softmax(y)$ is obtained and also what does it means)
	- during the learning also a BCE between $\tilde p$ and $softmax(y)$ is optimized, in order to avoid the estimated pseudo-truth label distribution $\tilde p$ from being totally different from the original noisy label distribution y
	- Authors try to control the pseudo distribution by encouraging the predicted label distribution to be sharpen for each sample. Under this purpose, another regularization term is introduced: the distribution sharpen constraint, which pushes the predicted probability of each type to nearly 0 or 1
	
The training strategy is divided in three phases: 

1)  Preliminary training. Since the proposed approach does not rely on any extra supervision, at the beginning of the entire training process, we first train a basic entity typing model with parameters $\theta$ only using the original noisy labels (can be treated as warm-up training)
2)  Probabilistic Automatic Relabeling. After a preliminary network is trained, we can step into the second phase and jointly estimate the pseudo label distribution $\tilde p$.
3)  Fine tuning. Finally, we normalize the estimated distribution $\tilde p$ to one-hot labels $\hat y$ by choosing one label with maximum value for each sample, and then the pseudo labels $\hat y$ are used for continuous fine-tuning the basic typing model

Approach is experimented on [[Dataset - Ren's BBN]][[Dataset - Ren's FIGER]][[Dataset - Ren's Ontonotes]]

#paper #model_robust_to_noise 