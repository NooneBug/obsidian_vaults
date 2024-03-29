https://ieeexplore.ieee.org/document/9283464

Abstract
---
In this paper, we make an empirical comparison of different pre-trained embeddings on the task of ultra-fine entity typing which has more than 10k types. We apply 7 kinds of pre-trained embedding to the typing model to prove whether the pre-trained embedding has a positive effect. The results indicate that almost all context-sensitive pre-trained embeddings improve the performance of models using Glove. The pre-trained embedding generated by BERT achieves the best performance in the Ultra-Fine dataset and OntoNotes dataset, which shows BERT has better capability to extract finer-grained information than other pre-trained models.

In order to observe the effect of the pre-trained models, we conducted an empirical study using 7 context-sensitive pre-trained word embeddings on the task of ultra-fine entity typing. We use the pre-trained word embedding generated by ELMo , BERT , OpenAI-GPT , GPT-2 , XLNet , RoBERTa, ALBERT  instead of the static Glove word embedding used in the existing research, respectively

Model
---
![[2020_wang_architecture.png]]

[[Encoders - Neural Based Models - ELMo based architectures]]
[[Encoders - Neural Based Models - BERT Based Architectures]]
#pretrained_word_embeddings_word2vec 
#encoder_with_attention 
#encoders_with_recurrent_architecture 

Evaluation
---

Models are evaluated on [[Dataset - UFET]] and [[Dataset - Ren's Ontonotes]]

---

Yanping Wang 
School of Computer Science and Technology Beijing Institute of Technology Beijing,

Xin Xin 
School of Computer Science and Technology Beijing Institute of Technology Beijing, 

Ping Guo 
School of Systems Science Beijing Normal University

#paper #encoder_with_attention #pretrained_word_embeddings_word2vec 