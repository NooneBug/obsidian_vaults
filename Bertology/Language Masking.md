One of the two pre-training methods used to train BERT on a large corpora (the other is [[Next Sentence Prediction]])

It consists of:
- Take a sentence
- Mask one word (with index *i*, (index 0 is for the \[CLS\])) with the token \[MASK\]
- Attach a classifier on the *i*-th output of the last transformer  