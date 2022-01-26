https://www.researchgate.net/publication/2500185_An_Algorithm_that_Learns_What's_in_a_Name

Presents a tool for Named Entity Extraction and Classification. Defines also metrics, classical Precision and Recall based on 

	- Correctness of identitdified boundaries of the named entity
	- Correctness of the classification

Defines the relation between a class occurrence (i.e. named entity) and its context:  

*All classes are contiguous sequences of words where local context usually contains enough information to identify the term as a class member.*

Presents a solution based on Hidden Markov Model and Handcrafted Features

It is the first approach in Entity Typing that uses Handcrafted features [[Encoders - Handcrafted Features  Based Models]], defining 14 features; each word is encoded using a ordered pairs <word, vector>:
		- word is a one-hot vector over the dictionary
		- vector is a 14-dimensional one-hot vector that describes handcrafted features 

Uses [[1995 Sundheim - Entity Task Definition (MUC-6)]] and [[1996 Merchant - The Multilingual Entity Task (MET) Overview]]

#paper