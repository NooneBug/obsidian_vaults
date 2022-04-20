[Medium post: introducing fastbert a simple deep learning library for bert models](https://medium.com/huggingface/introducing-fastbert-a-simple-deep-learning-library-for-bert-models-89ff763ad384)

BERT is fundamentally just a stack of encoders.

BERT Base:
- 12 Transformers
- 12 Self-attention heads

BERT popularized the Pre-train + Fine-tune architecture: 
- Pre train: Semi-supervised training on large amounts of texts, 
	- [[Language Masking]]
	- [[Next Sentence Prediction]] (binary, IsNext or NotIsNext)
- Fine-Tune: The pretrained BERT can be used as encoder on multiple tasks and fine-tuned on specific datasets by supervised training