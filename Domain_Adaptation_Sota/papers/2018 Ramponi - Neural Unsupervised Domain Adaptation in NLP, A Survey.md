https://arxiv.org/pdf/2006.00632.pdf

A default assumption in many machine learning algorithms is that the training and test sets follow the same underlying distribution. When these distributions do not match, we face a dataset shift [[2007 Gretton - A Kernel Method for the Two-Sample-Problem]] – in NLP typically referred to as a domain shift. In this setup, the target domain and the source training data differ, they are not sampled from the same underlying distribution. Consequently, performance drops on the target, which undermines the ability of models to truly generalize into the wild

Domain adaptation is closely tied to a fundamental bigger open issue in machine learning: generalization beyond the training distribution. Ultimately, intelligent systems should be able to adapt and robustly handle any test distribution, without having seen any data from it. This is the broader need for out-of-distribution generalization [[2019 Bengio - Deep Learning for AI]], and a more challenging setup targeted at handling unknown domains [[2018 Volpi - Generalizing to unseen domains via adversarial data augmentation]]; [[2020 Krueger -  Out-of-distribution generalization via risk extrapolation]].

Describes [[Domain Adaptation]]
Describes [[Supervised Domain Adaptation]]
Describes [[Unsupervised Domain Adaptation]]
Defines [[Domain  Adaptation Approaches Categories]]

Then describes [[What is a domain? Domain definitions]], comparing classic [[Domain Definition - Canonical vs Non-canonical]] with more versatile [[Domain definition - Variety Space]]

#paper