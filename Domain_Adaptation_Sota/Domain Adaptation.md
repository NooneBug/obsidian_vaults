From [[2018 Ramponi - Neural Unsupervised Domain Adaptation in NLP, A Survey]]: 

Domain adaptation aims to learn a function f from a source domain DS that generalizes well to a target domain DT , where the marginal probability over the feature space in the source is different from the one in target, i.e. the source and the target domain are defined by different samples of the variety space [[Domain definition - Variety Space]] DA is a particular case of transfer learning, namely  [[Transductive Transfer Learning]] [[2009 Pan - A Survey on Transfer Learning]] 

[[2019 Ruder - Neural Transfer Learning for Natural Language Processing]] defines domain adaptation as: 

In transductive DA, the source and target tasks TS and TT remain the same, but the source and target domains DS and DT differ in their underlying probability distributions. Given two distributions PS(X, Y ) and PT (X, Y ), DA typically addresses the shift in marginal distribution PS(X) != PT (X), also known as covariate shift. A related problem is the problem of label shift, PS(Y ) != PT (Y ). (extracted from [[2018 Ramponi - Neural Unsupervised Domain Adaptation in NLP, A Survey]])