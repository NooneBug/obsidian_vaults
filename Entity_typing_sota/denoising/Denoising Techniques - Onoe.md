proposed by [[2019 Onoe - Learning to Denoise Distantly-Labeled Data for Entity Typing]]

![[2019_onoe_filtering_relabeling_architecture.png]]

It is composed of two modules:

- A filtering module: given an input sentence and a set of labels, decides if maintain or filter out this example. This module is used to filter out the more problematic example
- Relabeling module: given an input sentence and a set of labels, outputs a new set of labels, combining the information from both inputs.

The filtering module is trained by generating a new training set:

- 30% of the data labels are substituted with a labelset with no incident labels
- The filtering module is trained to accept original data and to reject new one

The relabeling module is trained by generating a new training set:

- Each type of each example is dropped with a probability of 70%
- The relabeling module is trained to add these labels

Fun fact: the trained relabeling module often drop some input labels

The input encoder is the same used in [[2019 Onoe - Learning to Denoise Distantly-Labeled Data for Entity Typing]], the type encoder is composed of:

- Learn a representation for each type and treat a typeset as an unordered bag of word by summing the learned vectors
- Learn a representation using a BiLSTM on the GloVe representations of words in the wordnet definition of each type  #pretrained_word_embeddings_glove  and sum each representation like the previous point #encoders_with_recurrent_architecture 
- The type encoding is the concatenation of the two representations

The two new training module are obtained by the manually annotated dataset, the trained network is fed with the automatically annotated dataset to produce a new dataset [[Denoising Techniques - Modify the training set]]

