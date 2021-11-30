Encoder used firstly in [[2018 Xu - Neural Fine-Grained Entity Type Classification with Hierarchy-Aware Loss]] and then in other papers (linked to this note)

This approach represent words with [[Encoders - Pretrained Word Embeddings]] (GloVe)

- Mentions are represented by averaging [[Encoders - Pretrained Word Embeddings]] and also by LSTM [[Encoders - Neural Based Models - Recurrent architectures]]

- Contexts are represented through Bi-LSTM over word vectors [[Encoders - Neural Based Models - Recurrent architectures]][[Encoders - Pretrained Word Embeddings]] and word level attention [[Encoders - Neural Based Models - Attention based architectures]]