https://arxiv.org/pdf/2101.11212.pdf

*"In attempts to deal with the label noise, leading research on the FG-NET assumes that the fine-grained entity typing data possesses a euclidean nature, which restraints the ability of the existing models in combating the label noise. Given the fact that the fine-grained type hierarchy exhibits a hierarchical structure, it makes hyperbolic space a natural choice to model the FG-NET data. In this research, we propose FGNET-RH, a novel framework that benefits from the hyperbolic geometry in combination with the graph structures to perform entity typing in a performance-enhanced fashion. FGNET-RH initially uses LSTM networks to encode the mention in relation with its context, later it forms a graph to distill/refine the mention’s encodings in the hyperbolic space. Finally, the refined mention encoding is used for entity typing"*

Contributions
---
FGNET-RH follows a two-stage process, 

- (1) encode the mention along with its context using multiple LSTM networks, 
- (2) form a graph to refine mention’s encoding from (1) by sharing contextual information in the hyperbolic space. 

In order to maximize the benefits of using the hyperbolic geometry in combination with the graph structure, FGNET-RH maps the mention encodings (from (1)) to the hyperbolic space. And, performs all the operations: linear transformation, type-specific contextual aggregation etc., in the hyperbolic space, required for appropriate additive context-sharing along the type hierarchy to smoothen the noisy type-labels prior to the entity typing. 

The major contributions of FGNET-RH are enlisted as follows: 

1. FGNET-RH accommodates the benefits of: the graph structures and the hyperbolic geometry to perform fine grained entity typing over distantly supervised noisy data in a robust fashion. 
2. FGNET-RH explicitly allows label-smoothing over the noisy training data by using graphs to combine the type-specific contextual information along the type hierarchy in the hyperbolic space. 
3. Experimentation using two models of the hyperbolic space, i.e., the Hyperboloid and the Poincare-Ball, ´ shows that FGNET-RH outperforms the existing research by up to 3.5% in terms of strict accuracy.

"*To the best of our knowledge, we are the first to explore the combined benefits of the graph convolution networks in relation with the hyperbolic geometry for FG-NET over distantly supervised noisy data*"

"*we propose attentive type-specific contextual aggregation in the hyperbolic space to fine-tune the mention’s encodings learnt over noisy data prior to entity typing*"

This paper assumes [[Noise Definition - SIngle Path vs Multi-Path]]

Overview
---
![[2021_ali_architecture.png]]
Our proposed model, FGNET-RH, follows a two-step approach, labeled as stage-I and stage-II in the Figure 3. 

Stage-I follows text encoding pipeline to generate mention’s encoding in relation with its context. 

Stage-II is focused on label noise reduction, for this, we map the mention’s encoding (from stage-I) in the hyperbolic space and use a graph to share aggregated type-specific contextual information along the type-hierarchy in order to refine the mention encoding. Finally, the refined mention encoding is embedded along with the label encodings in the hyperbolic space for entity typing.

So this is a #model_robust_to_noise 

Encoder
---

The encoder is composed as:
- Mention encoding: LSTM
- context encoding: 2 BiLSTM
- postition encoding: 2BiLSTM

All these 5 representations are concatenated.

#encoders_with_recurrent_architecture 

Fine-Tuning the input encoding
---
"*we form a graph to cluster contextually-similar mentions and employ hyperbolic geometry to share the contextual information along the type-hierarchy.*" Follwing the alghorithm:

1. Construct a graph such that contextually and semantically similar mentions end-up being the neighbors in the graph. 
2. Use exponential map to project the noisy mention encodings from stage-I to the hyperbolic space. 
3. In the hyperbolic space, use the corresponding exponential and logarithmic transformations to perform the core operations, i.e., (i) linear transformation, and (ii) contextual aggregation, required to fine-tune the encodings learnt in stage-I prior to entity typing.

And so using the hyperbolic space to aggregate the encodings and denoise the representations

**Graph Construction**

For each entity type, we average out corresponding 1024d embeddings for all the mentions in the training corpus, to learn prototype vectors for each entity type. Later, for each entity type $t$, we capture type-specific confident mention candidates $cand_t$, following the criterion: $cand_t = cand_t ∪ men$ if $(cos(men, {Prototype_t}) ≥ δ) ∀men ∈ C; ∀t ∈ T,$ where $δ$ is a threshold. Finally, we form pairwise edges for all the mention candidates corresponding to each entity type, i.e., $\{cand\}^T_{t=1}$, to construct the graph G, with adjacency matrix A.

So after this passage a bipartite graph is constructed: on the 'left' there are the prototypical mentions that are similar to at least one prototype, on the 'right' there are the types. The mentions are linked to the types if they are similar to the type's prototype (cosine similarity over a threshold). 

This graph is then used to extract type-type attention weights through a Graph Embedding method (???) 

Loss
---
The loss function is very similar to the [[Ranking Loss - 2016 Ren - Partial Label Loss | 2016 Ren's one]]; so clean mentions representations are optimized to be closer to all correct types than to wrong, noisy mentions representations are optimized to be closer to ONE correct type than to other types

Experiments
---

The approach is evaluated on [[Dataset - Ren's BBN]], [[Dataset - Ren's Ontonotes]]

---
Muhammad Asif Ali,1 Yifang Sun,1 Bing Li,1 Wei Wang,1,2 

1School of Computer Science and Engineering, UNSW, Australia 
2College of Computer Science and Technology, DGUT, China

#paper #model_robust_to_noise #encoders_with_recurrent_architecture 