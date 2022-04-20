One of the two pre-training methods used to train BERT on a large corpora (the other is [[Language Masking]])

It consists of:
- Take two sentences
- Apply masking on one word for each sentence
- Attach the sentences with \[SEP\]
- Ask BERT to answer if the second sentence is the *next sentence* given the first

