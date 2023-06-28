The Unimib hosted version of Vicuna is used (13B)

For each dataset entry to answer the following procedure is used:

- Traduce the plain text into the prompt
- Perform a three POST request containing the question 
- Pick the 3 answers  `answer 1`, `answer 2, `answer 3`

The experiment cannot be repeated with exact same answers since temperature is set to $.9$, with temperature $=.01$ a deterministic behavior can be obtained
