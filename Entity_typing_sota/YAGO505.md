Dataset defined in [[2012 Yosef - HYENA, Hierarchical Type Classification for Entity Names]]

We start with five broad classes namely PERSON, LOCATION, ORGANIZATION, EVENT and ARTIFACT. Under each of these superclasses, we pick 100 prominent subclasses. The selection of subclasses is based on the population of the classes: we rank them in descending order of the number of YAGO entities that belong to a class, and pick the top 100 for each of the top-level superclasses. This results in a very fine-grained reference taxonomy of 505 types, organized into a directed acyclic graph with 9 levels in its deepest parts.

So this is a [[Datasets with 10 to 999 classes]] and a [[Datasets with hierarchical sets of types]]

Authors use [[Encoders - Handcrated Features  Based Models]] and SVM 

First paper to use [[Inference Method - Hierarchical Inference]]