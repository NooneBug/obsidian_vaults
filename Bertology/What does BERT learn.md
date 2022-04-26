It seems that datasets are too easy since:

- BERT learns shallow heuristics in NLI ([McCoy et al. 2019](https://aclanthology.org/P19-1334/), [Zellers et al 2019](https://arxiv.org/abs/1905.07830), [Jin et al. 2020](https://arxiv.org/abs/1907.11932)) 
- BERT learns shallow heuristics in reading comprehension ([Si et al 2019](https://arxiv.org/abs/1910.12391), [Rogers et al. 2020](https://ojs.aaai.org//index.php/AAAI/article/view/6398), [Sugawara et al 2020](https://arxiv.org/abs/1911.09241)) 

Some ideas to have harder datasets are:

- Having paraphrased questions on Q&A datasets
- Having adversarial test data with lexical overlap on NLI datasets

In [Generalization in NLI: Ways (Not) To Go Beyond Simple Heuristics](http://export.arxiv.org/pdf/2110.01518) authors try to use different architecture (siamese BERT, adapters, debiasing with HEX projection) to see which one generalizes better on hard datasets, none of them worked (all worst than Vanilla BERT)

In [Generalization in NLI: Ways (Not) To Go Beyond Simple Heuristics](http://export.arxiv.org/pdf/2110.01518) it is also shown that larger models generalize better (but have to be trained for longer)




