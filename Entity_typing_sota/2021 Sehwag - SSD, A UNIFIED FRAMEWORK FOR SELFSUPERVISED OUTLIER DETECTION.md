https://arxiv.org/pdf/2103.12051.pdf

When trained on a particular data distribution, referred to as in-distribution ¨ data, deep neural networks are known to fail against test inputs that lie far away from the training distribution, commonly referred to as outliers or out-of-distribution (OOD) samples (Grubbs, 1969; Hendrycks & Gimpel, 2017). This vulnerability motivates the use of an outlier detector before feeding the input samples to the downstream neural network modules. However, a key question is to understand what training information is crucial for effective outlier detection? Will the detector require fine-grained annotation of training data labels or even access to a set of outliers in the training process?

Can we design an effective out-of-distribution (OOD) data detector with access to only unlabeled data from training distribution?

In absence of data labels, we develop a cluster-conditioned detection method in the feature space. We first partition the features for in-distribution training data in m clusters. We represent features for each cluster as $Z_m$. We use k-means clustering method, due to its effectiveness and low computation cost. Next, we model features in each cluster independently, and calculate the following outlier score $(s_x) = min_m D(x, Z_m)$ for each test input $x$, where $D(., .)$ is a distance metric in the feature space. We discuss the choice of the number of clusters in Section 4.2.

#paper 