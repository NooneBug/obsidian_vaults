In this experiment a **support** relations has to be found

## Results T8 and T1  
- Truncated and non truncated prompts inputed to chatgpt seem to return the same correct answer ( $17/18$ )
- In $1/18$ cases non truncated prompt in chatgpt generated a non-answer (answer 1, q_choice) ($18 = 3 answers \times 3 descriptions \times 2 prompts$)
- q_attack results:
	- ChatGPT                  : 3/3, 
	- ChatGPT truncated : 3/3
	- Vicuna truncated     : 3/3,
- q_choice results:
	- ChatGPT                  : 2/3, 1 non-answer
	- ChatGPT truncated : 3/3
	- Vicuna truncated     : 2/3, 
- q_support results:
	- ChatGPT                  : 3/3, 
	- ChatGPT truncated : 3/3
	- Vicuna truncated     : 0/3, 
- Vicuna generated schizophrenic answer in 2/11 cases  

# Results T2 and T8
- Truncated and non truncated prompts inputed to chatgpt seem to return the same correct answer ( $17/18$ ), ($18 = 3 answers \times 3 descriptions \times 2 prompts$)
- q_attack results:
	- ChatGPT                  : 3/3, 
	- ChatGPT truncated : 3/3
	- Vicuna truncated     : 2/3, 1 non-answer
- q_choice results:
	- ChatGPT                  : 2/3, 1 non-answer
	- ChatGPT truncated : 3/3
	- Vicuna truncated     : 1/3, 1 non-answer
- q_support results:
	- ChatGPT                  : 3/3, 
	- ChatGPT truncated : 2/3
	- Vicuna truncated     : 3/3,