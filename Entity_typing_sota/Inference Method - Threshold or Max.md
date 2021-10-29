This inference method is introduced by [[2016 Shimaoka - An Attentive Neural Architecture for Fine-grained Entity Type Classification]]

At inference, the type k is predicted if yk is greater than 0.5 or yk is the maximum value ∀k ∈ K. The motivation of the former is that it acts as a cutoff, while the latter enforces the constraint that each mention is assigned at least one type.

