https://arxiv.org/pdf/2101.00345.pdf

https://github.com/yasumasaonoe/Box4Types.

*"Neural entity typing models typically represent fine-grained entity types as vectors in a high-dimensional space, but such spaces are not well-suited to modeling these types’ complex interdependencies. We study the ability of box embeddings, which embed concepts as d-dimensional hyperrectangles, to capture hierarchies of types even when these relationships are not defined explicitly in the ontology. Our model represents both types and entity mentions as boxes. Each mention and its context are fed into a BERT-based model to embed that mention in our box space; essentially, this model leverages typological clues present in the surface text to hypothesize a type representation for the mention. Box containment can then be used to derive both the posterior probability of a mention exhibiting a given type and the conditional probability relations between types themselves. We compare our approach with a vector-based typing model and observe state-of-the-art performance on several entity typing benchmarks. In addition to competitive typing performance, our box-based model shows better performance in prediction consistency (predicting a supertype and a subtype together) and confidence (i.e., calibration), demonstrating that the box-based model captures the latent type hierarchies better than the vector-based model does"*

*"In this paper, we describe an approach that represents entity types with box embeddings in a highdimensional space. We build an entity typing model that jointly embeds each entity mention and entity types into the same box space to determine the relation between them. Volumes of boxes correspond to probabilities and taking intersections of boxes corresponds to computing joint distributions, which allows us to model mentiontype relations (what types does this mention exhibit?) and type-type relations (what is the type hierarchy?). Concretely, we can compute the conditional probability of a type given the entity mention with straightforward volume calculations, allowing us to construct a probabilistic type classification model."*

![[2021_onoe_figure_1.png]]

*"Box embeddings naturally represent these kinds of hierarchies as shown in the right half of Figure 1. A box that is completely contained in another box is a strict subtype of that box: any entity exhibiting the inner type will exhibit the outer one as well. Overlapping boxes like Politician and Author represent types that are not related in the type hierarchy but which are not mutually exclusive. The geometric structure of boxes enables complex interactions with only a moderate number of dimensions (Dasgupta et al., 2020). Vilnis et al. (2018) also define a probability measure over the box space, endowing it with probabilistic semantics. If the boxes are restricted to a unit hypercube, for example, the volumes of type boxes represent priors on types and intersections capture joint probabilities, which can then be used to derive conditional probabilities"*

![[2021_onoe_architecture.png]]

The architecture is composed as follows:

- [[Encoders - Neural Based Models - BERT Based Architectures | Bert Encoder]]:  Cast the sentence as CLS mention SEP sentence SEP and use the CLS as representation
- [[Models with Type Representations | Type Encoder]]: each type has a runtime learned box (a Gumbel Box)

Inference methods:

Given an input box, a score for each type is computed by computing the volume of the intersection of the boxes divided by the volume of the type box. The obtained score is then thresholded to infer the type.

The learning is optimized with ADAM on BCE

The model is experimented on [[Dataset - Ren's BBN]][[Dataset - Ren's FIGER]][[Dataset - Ren's Ontonotes]][[Dataset - UFET]]

Very good ablation study on box robustness to noisy and other things

---

Yasumasa Onoe♠, Michael Boratko♢, Andrew McCallum♢♣, Greg Durrett♠ 

♠The University of Texas at Austin 
♢University of Massachusetts Amherst 
♣Google Research

#paper 