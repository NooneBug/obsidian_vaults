Hierarchical Inference Method from [[2020 Ren - Fine-Grained Entity Typing with Hierarchical Inference]]:

![[2020_ren_architettura.png]]

The network has as many inference layer as the levels in the hierarchy (in the image 3 layers).

Each layer $L_i$ has:

- A representation $u_i$ obtained through a linear layer on the input representation;
- A representation $s_i$ obtained through a linear layer on $u_i$ and another linear layer on $s_{i-1}$, with ReLu
- A representation $y_i$ obtained through a linear layer on $s_i$

So here he hierarchy information is represented through is the information in $s_i$, and so **it is not explicit**

#inference_method 