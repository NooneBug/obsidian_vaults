[[2016 Ma - Label Embedding for Zero-shot Fine-grained Named Entity Typing]]

For top k type candidates, we greedily remove the labels that conflict with others. However, unlike [[Inference Method - Hierarchical Inference - 2015 Yogatama]], we use a relative threshold t to decide whether the selected type should remain in the final results, which is more consistent with the margin-infused objective function than a global threshold. Namely, a type candidate will be passed to type inference only if the difference of score from the 1-best is less than a threshold.

#inference_method 