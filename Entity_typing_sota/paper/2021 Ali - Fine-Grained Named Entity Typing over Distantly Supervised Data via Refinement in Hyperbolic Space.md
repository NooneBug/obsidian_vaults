https://arxiv.org/pdf/2101.11212.pdf

*"In attempts to deal with the label noise, leading research on the FG-NET assumes that the fine-grained entity typing data possesses a euclidean nature, which restraints the ability of the existing models in combating the label noise. Given the fact that the fine-grained type hierarchy exhibits a hierarchal structure, it makes hyperbolic space a natural choice to model the FG-NET data. In this research, we propose FGNET-RH, a novel framework that benefits from the hyperbolic geometry in combination with the graph structures to perform entity typing in a performance-enhanced fashion. FGNET-RH initially uses LSTM networks to encode the mention in relation with its context, later it forms a graph to distill/refine the mention’s encodings in the hyperbolic space. Finally, the refined mention encoding is used for entity typing"*

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

---
Muhammad Asif Ali,1 Yifang Sun,1 Bing Li,1 Wei Wang,1,2 

1School of Computer Science and Engineering, UNSW, Australia 
2College of Computer Science and Technology, DGUT, China