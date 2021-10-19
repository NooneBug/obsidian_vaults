From [[2020 Kashyap - Domain Divergences, A Survey and Empirical Analysis]]:

Standard machine learning models do not perform well when tested on data from a different target domain. The performance in a target domain largely depends on the domain divergence (Ben-David et al., 2010) – a notion of distance between the two domains. Thus, efficiently measuring and reducing divergence is crucial for adapting models to the new domain — the topic of domain adaptation. Divergence also has practical applications in predicting the performance drop of a model when adapted to new domains [[2010 Van Asch - Using Domain Similarity for Performance Estimation]], and in choosing among alternate models (Xia et al., 2020).

Domain Divergence helps in **Decisions in the Wild**: helps practitioners predict the performance or drops in performance of a model in a new target domain [[2020 Kashyap - Domain Divergences, A Survey and Empirical Analysis]]

[[2020 Kashyap - Domain Divergences, A Survey and Empirical Analysis]] classify divergence methods in: 
	- **Geometric measures** calculate the distance between two vectors in a metric space. As a divergence measure, they calculate the distance between features (tf.idf, continuous representations, etc.) extracted from instances of different domains
	- **Information- theoretic **measures the distance between probability distributions
	- **Higher-order** measures the distance between distributions considering higher moments or the distance between representations or their projections in a nonlinear space