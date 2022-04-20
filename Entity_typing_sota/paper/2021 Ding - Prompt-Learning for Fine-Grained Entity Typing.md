https://arxiv.org/pdf/2108.10604.pdf


Abstract
---
In this work, we investigate the application of prompt-learning on fine-grained entity typing in fully supervised, few-shot and zero-shot scenarios. We first develop a simple and effective prompt-learning pipeline by constructing entity-oriented verbalizer and templates and conducting masked language modeling. Further, to tackle the zero-shot regime, we propose a self-supervised strategy that carries out distribution-level optimization in prompt-learning to automatically summarize the information of entity types

Method
---

![[2021_ling_idea.png]]

Authors propose to use prompts to generate labels (similar to [[2021 Dai - Ultra-Fine Entity Typing with Weak Supervision from a Masked Language Model | weak label generation]]) and to optimize the language model to produce the correct labels based on the prompts

Authors inspects three prompt hard-template and one soft-template and optimize the network to predict the words in a restricted vocabulary. In this restricted vocabulary each word is mapped with one type in the dataset.

![[2021_ling_templates.png]]
![[2021_ling_templates2.png]]

Authors propose to train this method both on supervised entity typing (optimizing the labels), and with self-supervising (optimizing the similarity between the predictions for sentences with the same entity mention)

![[2021_ling_self_supervised.png]]

Experiments
---
Method is experimented on FEW-NERD, [[Dataset - Ren's BBN]] and [[Dataset - Ren's Ontonotes]] both in zero-shot, few shot and supervised
___
Ning Ding1 , 
Yulin Chen3 , 
Xu Han1,5 , 
Guangwei Xu2 , 
Pengjun Xie2 , 
Hai-Tao Zheng3 , 
Zhiyuan Liu1,5 , 
Juanzi Li1 , 
Hong-Gee Kim4 

1Department of Computer Science and Technology, Tsinghua University 
2 Alibaba Group 
3 SIGS, Tsinghua University 
4 Seoul National University 
5 State Key Lab on Intelligent Technology and Systems, Tsinghua University

#paper 