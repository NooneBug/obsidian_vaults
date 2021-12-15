Distant supervision is a technique to obtain annotated data without the direct action of a human. Generally use a restricted set of manually curated annotated examples to approximate / learn the annotation procedure and then is used to produce a high number of automatically annotated examples


In [[2021 Dai - Ultra-Fine Entity Typing with Weak Supervision from a Masked Language Model | 2021 Dai]] there are two critics of common Distant supervision methods in FGET datasets:

Several problems exist when using these weak labels for the ultra-fine typing task. 
- First, in the dataset created by [[Dataset - UFET | Choi et al. (2018)]], on average there are fewer than two labels (types) for each sample annotated through either entity linking or head word supervision. On the other hand, a human annotated sample has on average 5.4 labels. As a result, models trained from the automatically obtained labels have a low recall. 
- Second, neither of the above approaches can create a large number of training samples for pronoun mentions. 
- Third, it is difficult to obtain types that are highly dependent on the context. For example, in “I met the movie star Leonardo DiCaprio on the plane to L.A.,” the type passenger is correct for “Leonardo DiCaprio.” However, this type cannot be obtained by linking to knowledge bases.
 