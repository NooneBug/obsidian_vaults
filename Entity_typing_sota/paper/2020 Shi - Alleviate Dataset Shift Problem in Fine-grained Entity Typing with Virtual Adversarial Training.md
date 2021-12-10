https://www.ijcai.org/Proceedings/2020/0539.pdf

*"the heuristically generated labels inevitably bring a significant distribution gap, namely dataset shift, between the distantly labeled training set and the manually curated test set. Considerable efforts have been made to alleviate this problem from the label perspective by either intelligently denoising the training labels, or designing noise-aware loss functions. Despite their progress, the dataset shift can hardly be eliminated completely"*

*In this work, complementary to the label perspective, we reconsider this problem from the model perspective: Can we learn a more robust typing model with the existence of dataset shift? To this end, we propose a novel regularization module based on virtual adversarial training (VAT). The proposed approach first uses a self-paced sample selection function to select suitable samples for VAT, then constructs virtual adversarial perturbations based on the selected samples, and finally regularizes the model to be robust to such perturbations.*

*"All the previous denoising methods are dedicated to reduce the gap of joint distribution $P(y, x)$ between the training set and test set, that is, the dataset shift $∆$s in Figure 1. However, since it is impossible to completely eliminate the dataset shift in distantly-supervised FET, the test loss can still be large even we achieve the minimum loss on the training set. Specifically, the denoising methods try to get low test loss by solving $argminθ f(∆s|θ)∗ f(Ltrain|θ$). As is shown in Figure 1, even though the model achieves the minimum loss on the training set at $θ$s and the dataset shift is reduced to a small value $∆$s, the test loss can still be large."*

![[2020_shi_figure_1.png]]

*"In this work, complementary to the label perspective, we reconsider this problem from the model perspective: Can we learn a more robust typing model with the existence of dataset shift? As is shown in Figure 1, when dataset shift $∆s \neq 0$ is fixed, test loss not only depends on training loss $f(Ltrain|θ)$ but also depends on the gap ∆L between test loss and training loss. Therefore, we propose to learn a robust typing model by solving $argminθ f(∆L|∆s, θ) ∗ f(∆s|θ) ∗ f(Ltrain|θ)$, where $f(∆L|∆s, θ)$ is a measure of the generalization ability and robustness to dataset shift of models"*

The major contributions of this paper are summarized as follows: 

1. This work provides a new perspective on the problems caused by distant supervision for fine-grained entity typing and explores a new way to improve FET systems by regularizing the model to be robust to dataset shift. 
2. A novel regularization module for FET is proposed, where a variant of VAT and a sample selection function is proposed to control the robustness of typing model. 
3. Extensive experiments on standard benchmarks with two different base models demonstrate that our method brings stable and significant improvement over the base models. Finally, the proposed method consistently outperforms several state-of-the-art (SOTA) FET systems by a significant margin.

In this approach [[Dataset Modification - 2018 Xu - Multilabel to single label | the same assumptions]] of [[2018 Xu - Neural Fine-Grained Entity Type Classification with Hierarchy-Aware Loss | 2018 Xu]] holds, so the multilabel problem is casted in a single label problem. To do this [[Noise Definition - SIngle Path vs Multi-Path | Single Path labels are considered clean]] and the other are considered noisy

**Approach**

The approach is mainly based on the following assumption: the model should predict smoothly around the mention points in the feature space because mention points close to each other in feature space have similar context.

The approach experimented two different input encoders: 

- [[Xu Encoder]]
- [[Encoders - Neural Based Models - BERT Based Architectures | BERT]]

The classifier is composed as: With the representation zi of a mention with its context, we employ a softmax classifier to get the posterior: $P(y|z_i) = softmax(W_c*z_i + b_C )$, where $W_C ∈ R^{K×d_z}$ can be treated as the type embeddings, $b_c ∈ R^{d_z}$ is the type bias, where K is the number of types. The predicted type $\hat y$ is the type with maximum posterior probability: $\hat y = arg max_y P(y|z_i)$. So this is a [[Models with Type Representations | Model with Type Representations]] and predict [[Predictions - Single Path Prediction | Single Path Prediction]] and [[Predictions - Partial Path Prediction | Partial Path Prediction]].

**Dataset Shift**
The dataset shift problem is faced with adversarial training. Each encoded input is evaluated to express how noisy is (see the paper, Sample Selection paragraph). Then for each sample, KL divergence is computed between:

-	The actual prediction
-	The prediction given by the same encoded input plus a perturbation based on an example elected at the previous phase

Then virtual adversarial is used (*very complex, more study needed in this domain*)

Approach is experimented on [[Dataset - Ren's BBN]] and [[Performances - Ren's Ontonotes]]

#paper 