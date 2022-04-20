Reminding the lottery ticket hypotesis: *"Dense, randomly-initialized, feed-forward networks contain subnetworks (winning tickets) that, when trained in isolation, reach test accuracy comparable to the original network in a similar number of iterations"*

In the paper [When BERT Plays the Lottery, All Tickets Are Winning](https://aclanthology.org/2020.emnlp-main.259.pdf) the lottery ticket hypotesis is changed a bit: *"Pre-trained trasnformers contain subnetworks (winning tickets) that, when trained in isolation, reach test accuracy comparable to the original network in a similar number of iterations"*  and is experimented with different methods:

Method 1 - unstructured magnitude pruning (m-pruning): procedure in two steps:

1. Iteratively prune 10% of the least magnitude weights across the entire fine-tuned model (except the embeddings) and evaluate on dev set
2. Repeat (1) so long as performance of the pruned subnetwork is above the 90% of the full model

Method 2 - structured pruning heads and MLPs based on importance scores (s-pruning): 

1. Iteratively prune 10% of the least magnitude heads and the least important MLP inside the transformer (*not so clear how evaluated, see the [paper](https://arxiv.org/pdf/1905.10650.pdf)*) and evaluate on dev set
2. Repeat (1) so long as performance of the pruned subnetwork is above the 90% of the full model

Outcomes
---

m-pruning does not extracted winning tickets, method 2 instead does extracted winning tickets

m-pruning is quite stable, the std of the obtained results is .01 across 5 random seeds

s-pruning is very unstable (.55 std across 5 random seeds)
The reason of unstableness of s-pruning is that most heads are about equally uninmportant
subnetworks found with s-pruning are not stable (not every time the same subnetwork) across related tasks

The Good, the Bad and the Random
---
Experiment to see how bad are the bad subnetworks?

Different subnetworks composed by elements (weights, heads, and MLP) are examinated:
- The Good: elements selected from the full model by either pruning strategy
- The Bad: elements that did not survive the pruning and few sampled from the remaining to mathc *the Good* subnetwork size 
- The Random: elements randomly sampled from the full model to match *the Good* subnetwork size

Results on all GLUE tasks show that:
- m-pruning : In regression tasks (CoLA and STS-B) performance by the Bad and the Random are very worst than performance by the Good
- m-pruing : In other tasks a similar pattern is observed but not so drastical like the regression tasks
- s-pruning : all models have similar performance (all tickets are winning)


The [same paper](https://aclanthology.org/2020.emnlp-main.259.pdf) shows also that [[How important are attention heads?|heads patterns]] surviving importance-based pruning are not necessarily linguistically informative

