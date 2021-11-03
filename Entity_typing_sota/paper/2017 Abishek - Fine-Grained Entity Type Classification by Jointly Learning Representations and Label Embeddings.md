https://arxiv.org/pdf/1702.06709.pdf

*Existing FETC systems have two major drawbacks: assuming training data to be noise free and use of hand crafted features. Our work overcomes both drawbacks. We propose a neural network model that jointly learns entity mentions and their context representation to eliminate use of hand crafted features. Our model treats training data as noisy and uses non-parametric variant of hinge loss function*

Use [[Noise Definition - SIngle Path vs Multi-Path]]

Propose a model based on recurrent architecture [[Encoders - Neural Based Models - Recurrent architectures]] composed of

	- an LSTM to encode mention tokens
	- two bi-LSTM to encode left and right contexts
	
Then concatenates the three representations

Propose a model with runtime learnt type representation [[Models with Type Representations]] and use dot product as score function 

Use a special loss function : [[Special Hinge Loss - 2017 Abishek ]] thus it is a [[Models Robust to Noise]]

The inference method is the [[Inference Method - Hierarchical Inference - 2016 Ren]] with fixed threshold

This work is the first in which [[Transfer Learning in ET]] is proposed, authors train their model on [[Dataset - Ren's FIGER]] and use the obtained representation as input for [[2016 Ren - AFET, Automatic Fine-Grained Entity Typing by Hierarchical Partial-Label Embedding]]

The method is evaluated on [[Dataset - Ren's BBN]], [[Dataset - Ren's FIGER]], [[Dataset - Ren's Ontonotes]]

#paper  