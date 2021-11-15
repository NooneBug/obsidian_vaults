Extracting informations from multiple documents wiil be so usefull to help humans to have summary of the information

MultiDocument Language models (based on BERT) where defined

- the training is performed as a masked language model with parallel inputs, the information to complete the cloze may come from other document (where they are explicitly described)
- the trained is composed of
	- parallel documents that talks about the same topic
	- parallel documents that talks about different topics
	- single documents
		
Usefull multidocument tasks

- Multi document summarization

- multi document information extraction 
	- information has to be matched in some way
	- maybe only some sentences contain the same information and so it was deinfed sentence-level matching
	
- how to represent information unit? 
	- the spans that define an information has to be as precise as possible
	-  information in text can be represented as a list of questions that can be answered by reading the text
		-  How to select relevant information? (open question)

#sunday
#allenai