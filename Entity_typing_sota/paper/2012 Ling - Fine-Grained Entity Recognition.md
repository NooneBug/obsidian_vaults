http://aiweb.cs.washington.edu/ai/pubs/ling-aaai12.pdf

Defines [[FIGER]], a dataset for Fine Grained Entity Recognition / Typing 

*There are three challenges impeding the development of a fine-grained entity recognizer: selection of the tag set, creation of training data, and development of a fast and accurate multi-class labeling algorithm. We address the first challenge by curating a set of 112 unique tags based on Freebase types. The second challenge, creating a training sets for these tags, is clearly too large to rely on traditional, manual labeling. Instead, we exploit the anchor links in Wikipedia text to automatically label entity segments with appropriate tags. Next, we use this heuristically-labeled training data to train a conditional random field (CRF) model for segmentation (identifying the boundaries of text that mentions an entity). The final step is assigning tags to the segmented mentions; for this purpose, we use an adapted perceptron algorithm for this multi-class multi-label classification problem. We call the complete system FIGER.*

They used the predicted types in downstream to enhance relation extraction algorithms

Defines clearly what a mention is and the relation with its types: 

*Our task is to uncover the type information of the entity mentions from natural language sentences. Formally speaking, we need to identify the entity mentions {m1, . . . , mk}, such that each mi is a subsequence of s,as well as associate the correct entity types, ti with each mi*

Authors also define a perceptron based model to produce [[Predictions - Multiple Path Precition]] starting from [[Encoders - Handcrated Features  Based Models]]

#paper 