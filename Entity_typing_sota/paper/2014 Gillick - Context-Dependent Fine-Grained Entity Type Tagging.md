https://arxiv.org/pdf/1412.1820.pdf

First paper to explicitly define "context dependent entity typing" i.e. where the set of acceptable labels for a mention is restricted to only those deducible from the local context (e.g. sentence or document).

The authors propose a new dataset for fine grained entity typing: [[Dataset - Ontonotes v5 - GFT]]

This is the first paper that try to apply [[Denoising Techniques - Modify the training set]] on the training set [[Denoising Techniques - Gillick 2014 Rules]]

Authors define a model to perform Entity Typing: each sentence is represented through a [[Encoders - Handcrafted Features  Based Models]] and a topic model on the document *training a simple bag-of-words topic model with eight topics (arts, business, entertainment, health, mayhem, politics, scitech, sport)*

Authors experiments both local classifier (one binary classifier for each label, label consinstency is forced at test time) and flat classifier (one classifier for all labels)

They found that local outperforms flat

#paper 