This is a [[Ranking Loss]] used in [[2016 Ren - AFET, Automatic Fine-Grained Entity Typing by Hierarchical Partial-Label Embedding]]

Hypothesis 1 (Adaptive Margin) For a mention, if a negative type is correlated to a positive type, the margin between them should be smaller

Adaptive margin is computed based on a type correlation notion, the idea is the following:

*If the correct type is C and an uncorrect type is U, I want that the entity mention representation is more similar to C than to U at least by an adaptive margin that depends on the correlation between C and U (the higher the correlation, the lower the adaptive margin) *

Hypothesis 2 (Partial-Label Loss) For a noisy mention, the maximum score associated with its candidate types should be greater than the scores associated with any other non-candidate types

*The above idea is valid for ALL correct types for a clean mention, for only one (the one with maximum score), for a noisy mention*

Clean and noisy are referred to [[Noise Definition - SIngle Path vs Multi-Path]]
