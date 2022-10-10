https://aclanthology.org/2022.acl-long.141.pdf

(i) This study provides fresh insight into instance dependent label noise in FET. We pointed out a novel training method to further exploit feature space and global information. 
(ii) We designed a framework with feature clustering, estimating cluster-level confusion matrix, and loss correction. 
(iii) We experimented the proposed method on three datasets. Results show that we made significant improvements over previous state-of-the-art, thus proving the effectiveness of our model. Ablation studies further prove the robustness and wide applicability of our framework.

Use a backbone model trained on noisy dataset to produce input representation.

Cluster input representation from backbone model with K-Means. Evaluate the *pureness* of each cluster with respect to *trusted data* (not clear from where these trusted data are taken)

Estimate a loss correction using transition matrix estimation based on clusters.

Based on [[2018 Xu - Neural Fine-Grained Entity Type Classification with Hierarchy-Aware Loss|2018 Xu]] architecture 

Experimented on [[Dataset - Ren's BBN]], [[Dataset - Ren's FIGER]], [[Dataset - Ren's Ontonotes]]

#paper 
