https://arxiv.org/pdf/2106.04098.pdf

Abstract
---

"*there is an effort to extend fine grained entity typing by using a richer and ultra-fine set of types, and labeling noun phrases including pronouns and nominal nouns instead of just named entity mentions. A key challenge for this ultra-fine entity typing task is that human annotated data are extremely scarce, and the annotation ability of existing distant or weak supervision approaches is very limited. To remedy this problem, in this paper, we propose to obtain training data for ultra-fine entity typing by using a BERT Masked Language Model (MLM). Given a mention in a sentence, our approach constructs an input for the BERT MLM so that it predicts context dependent hypernyms of the mention, which can be used as type labels*"

---

In this paper there are [[Distant Supervision |critics]] to how distant supervision is used in FGET datasets building procedures

---

[[2021 Dai Literature References |The related work is very complete]]

Contributions
---
1. We propose a new way to generate weak labels for ultra-fine entity typing.
2. We propose an approach to make use of the newly obtained weak labels to improve entity typing results. 
3. We conduct experiments on both an ultra-fine entity typing dataset and a traditional fine grained entity typing dataset to verify the effectiveness of our method

Approach
---
The authors use BERT MLM task to produce contextual candidate labels by masking the entity mention

Our methodology consists of two main steps. First, we obtain weak ultra-fine entity typing labels from a BERT masked language model. Second, we use the generated labels in model training to learn better ultra-fine entity typing models

MLM are fed with inputs modificated with Hears patterns: *“In late 2015, Leonardo DiCaprio starred in The Revenant.” To find the hypernym or the type of “Leonardo DiCaprio”, we insert three tokens to create a “such as” pattern: “In late 2015, [MASK] such as Leonardo DiCaprio starred in The Revenant.” Applying the BERT MLM on the sentence, we derive hypernyms such as “actors,” “stars,” “directors,” “filmmakers.”* 63 Hearts-like patterns are used.

Weak labels are singularized and then filtered using the type vocabulary of the dataset ([[Dataset - UFET]]). Finally the most probable $k$ different weak labels are taken 

The different Hearst-like patterns can generate very different labels, *to address the above problem, we do not use a same pattern for all the mentions. Instead, for each mention, we try to select the best pattern to apply from a list of patterns. This is achieved by using a baseline ultra-fine entity typing model, BERT-Ultra-Pre, which is trained beforehand without using labels generated with our BERT MLM based approach. Denote the pattern list as L. With each pattern in L, we can apply it on the given mention to derive a set of labels from the BERT MLM. Then, we find the set of labels that have the most overlap with the labels predicted by BERT-Ultra-Pre. Finally, the given mention is annotated with this set of labels*

The 63 patterns are filtered using this procedure: 

- Step 1: Initialize L to contain the best performing pattern (i.e., “M and any other H”) only. 
- Step 2: From all the patterns not in L, find the one that may bring the greatest improvement in F1 score if it is added to L. 
- Step 3: Add the pattern found in Step 2 to the L if the improvement brought by it is larger than a threshold. 
- Step 4: Repeat steps 2-3 until no patterns can be added.

The authors also depict that if the BERT MLM vocabulary does not cover all types in the datasets then this approach is sub-optimal; they report that 92% of types are covered by the vocabulary

The weak labels are used only for named entity and nominal mentions, not for pronouns

Architecture
---
The trained model is [[2019 Onoe - Learning to Denoise Distantly-Labeled Data for Entity Typing | 2019 Onoe]]; [[Losses - Choi Loss | Choi Loss]] is used. The loss on weak labels and on original labels have different weights

Experiments
---
The model is evaluated on [[Dataset - UFET]] and [[Dataset - Ren's Ontonotes]]

Analyze the differences in performances based on the kind of entity mention: named entity, pronoun and nominal

Hongliang Dai,(1) 
Yangqiu Song (1)
Haixun Wang (2)

(1) Department of CSE, HKUST 
(2) Instacart

#paper 