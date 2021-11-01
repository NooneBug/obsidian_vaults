[[2015 Yogatama - Embedding Methods for Fine Grained Entity Type Classification]]

*"During inference, we consider the top-k predicted labels, where k is the maximum depth of the label hierarchy, and greedily remove labels that are not consistent with other labels (i.e., not on the same path of the tree)"*. Authors also use a threshold to stop the inference before reaching k consinstent labels.

#inference_method