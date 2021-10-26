https://aclanthology.org/P15-2048.pdf

Authors *"propose a new approach to the task of fine grained entity type classifications based on label embeddings that allows for information sharing among related labels. Specifically, learn an embedding for each label and each feature such that labels which frequently co-occur are close in the embedded space."*

First [[Models with Type Representations]]: similarly to WSABIE (Weston 2011) authors use a matrix to represent each type.

Given an entity mention in a sentence, the entity mention is encoded with [[Encoders - Handcrated Features  Based Models]], then a score for each type is computed by computing dot product with type representation 

Authors use ranking loss to encourage the model to place positive labels above negative labels without competing with each other 

For inference the authors use [[Inference Method - Hierarchical Inference]]:*"During inference, we consider the top-k predicted labels, where k is the maximum depth of the label hierarchy, and greedily remove labels that are not consistent with other labels (i.e., not on the same path of the tree)"*. Authors also use a threshold to stop the inference before reaching k consinstent labels. So this model produces [[Predictions - Single Path Prediction]] and allow [[Predictions - Partial Path Prediction]]

Experiments use [[Dataset - FIGER]] and [[Dataset - Ontonotes v5 - GFT]]

#paper