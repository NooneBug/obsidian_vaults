hierarchModels that use encoders based on BERT (Devlin 2019)

[[2020 Wang - An Empirical Study of Pre-trained Embedding on Ultra-Fine Entity Typing]] benchmarked contextual encoders and prove that BERT based encoders are the best for FGET

[[2020 Shi - Alleviate Dataset Shift Problem in Fine-grained Entity Typing with Virtual Adversarial Training]] Cast the sentence as CLS context SEP mention SEP and use the CLS as representation

[[2020 Dai - Exploiting Semantic Relations for Fine-grained Entity Typing]] cast the sentence as CLS sentence SEP mention SEP

[[2021 Dai - Ultra-Fine Entity Typing with Weak Supervision from a Masked Language Model]]  use BERT to obtain types by masking the entity mention in the input sentence and optimizing the generated tokens to obtain tokens that represent the correct types

[[2021 Onoe - Modeling Fine-Grained Entity Types with Box Embeddings]]
Cast the sentence as CLS mention SEP sentence SEP and use the CLS as representation

[[2021 Hou - Transfer learning for fine-grained entity typing]]
SpanBERT to represent the context

[[2021 Liu - Fine-grained Entity Typing via Label Reasoning]] uses bert with special tokens for entity start and entity end and use CLS as encoding

#encoder 