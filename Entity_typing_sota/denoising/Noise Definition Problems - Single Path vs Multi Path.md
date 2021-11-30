The [[Noise Definition - SIngle Path vs Multi-Path]] has some problems, because do not consider these scenarios:

	- In BBN/FIGER there are root types that share a lot of entities (/GAME and /PRODUCT, or /LOCATION and /GPE (geopolitical entity)), 
	- In the same sentence, a mention can have as much information to belong to siblings (e.g., "the lawyer and former president Barack Obama")

This definition will treat these correct annotations as noisy one, and cannot predicts the correct set of labels 

Also [[2020 Zhang - Learning with Noise, Improving Distantly-Supervised Fine-grained Entity Typing via Automatic Relabeling]] report another major problem of this definition: "*(models are ) incapable of eliminating the impact of samples with only one type label but are false positive*" 