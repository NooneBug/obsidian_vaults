https://pure.rug.nl/ws/portalfiles/portal/128652251/aac_2020_11_1_2_aac_11_1_2_aac200901_aac_11_aac200901.pdf

### Introduction

Given the multiform nature of arguments and argumentation, the question arises on whether it is possible to develop general purpose and largely applicable theoretical and computational tools for it.

While each individual argument could be regarded as acceptable in isolation, it is clear that they cannot be accepted all together because, for instance, it is impossible to be vegetarian and not vegetarian at the same time or to adopt and not to adopt a vaccination program at the same time.

Different argumentation contexts share a fundamental question, namely identifying which arguments are acceptable and an essential feature, namely that arguments attack each other. Abstract argumentation, described in the next section, adopts the standpoint that this essential feature is a sufficient basis to define a general formalism able to provide answers to the fundamental question of acceptability of any set of arguments

### [[1995 Dung - On the acceptability of arguments and its fundamental role in nonmonotonic reasoning, logic programming and n-person games|Abstract argumentation]]

Abstract argumentation has been originally proposed in an effort to understand how common people, many of them may even be illiterate, carry out their reasoning. While abstract argumentation could be viewed as a formalism for capturing various approaches to commonsense reasoning (in particular non-monotonic reasoning and cooperative games), it is also a methodology for providing abstractions of problems along three dimensions:
- arguments, 
- attacks 
- acceptability, 
	- what agents have to accept given what they know (i.e. the arguments and associated attacks)

**Arguments:** 
AI researchers recognized in the seventies and eighties that we need more than mathematical arguments to build practical reasoning systems, in particular in logic programming and non-monotonic logic. The structure of arguments may be complex in general, and different argumentation models choose different structures for arguments. Different models use different representations of the structure of those arguments, using reasons, rules, assumptions, logical deductions in various combinations.

**Attack**: 
The notion of attack is core in abstract argumentation, as without disagreement there is no arguing. Attacks may originate from several sources and indeed several types of attack have been identified in the literature. In particular, often rebuttal and undercutting attacks are distinguished (following [Pollock](https://onlinelibrary.wiley.com/doi/epdf/10.1207/s15516709cog1104_4)): the rebutting type unearths disagreement between arguments with conflicting conclusions, whereas the undercutting type emphasizes an attack on the connection between reason and conclusion. Different argumentation models use alternative ways to include kinds of attack, sometimes distinguishing more kinds, sometimes reducing different kinds to a single formal structure.

**Argument acceptance**: 
A cornerstone of abstract argumentation is that argument acceptance can be evaluated taking into account the attack relation only, independently of any other underlying detail, thus ensuring a uniform applicability to a wide variety of situations. Intuitively, arguments are accepted if they can be defended against attacks. 
	- For instance, if an argument $P$ is attacked by an argument $Q$, the first argument can be defended against the attack by a third argument $R$ that attacks the second argument $Q$. By itself, the argument $P$ would be successfully attacked or defeated by $Q$, but, considering also the counterattack by $R$, the argument $Q$ is no longer defeated and said to be reinstated. As a pair, the arguments $P$ and $R$ can withstand the attack by $Q$. 
In abstract argumentation, this idea of **a collection of arguments that can defend themselves against attack is captured in the central notion of an admissible set**. An admissible set of arguments is a set that contains no arguments that attack themselves or other arguments in the set and that contains a counterattack against all attack of arguments in the set.
	- For instance, the set consisting of the arguments $P$ and $R$ is admissible since $P$ and $R$ do not attack each other (or themselves) and $R$ defends $P$ against the attack by $Q$. The set consisting of only $P$ is not admissible since there is no defence against $Q$, and the set consisting of $P$ and $Q$ is not since $Q$ attacks $P$.

In abstract argumentation, several special kinds of admissible set are distinguished, referred to as **[[Argument Extension|extensions]]**, expressing different perspectives on the arguments that are collectively acceptable.
 - **Stable extensions**. A stable extension is a set of arguments that contains no arguments that attack each other and that also attacks every argument that is not in the set. 
	 - Given a stable extension, one could say that all conflicts between arguments are resolved: either an argument is in the collectively defensible set, or it is attacked by the set. 
	 - Stable extensions do not always exist, and sometimes there are many of them, suggesting alternative ways of resolving conflicts. 
	 - For instance, the attacks between the example arguments A, B, C and D lead to three alternative stable extensions, one in which A and C are accepted, one containing A and D, and the third one B and D.
![[2020_baroni_fig1.png]]
 - **Preferred extensions.** A preferred extension is a set that is a maximal admissible set, in the sense that after adding any additional argument the set is no longer admissible. 
	 - There always exists at least one preferred extension – even when there is no stable extension, suggesting a way to solve as many conflicts as possible. 
	 - Like for stable extensions, there can be several alternative preferred extensions. 
	 - In the example, there are three preferred extensions, coinciding with the stable extensions.
 - **Grounded extensions.** The grounded extension – there is always exactly one – expresses a set of acceptable arguments about which there is no ambiguity. 
	 - The grounded extension can be constructed by accepting all arguments that are not attacked at all, then adding all arguments that are defended by the already accepted arguments, and so on. 
	 - In the example, the grounded extension is empty, since all arguments are attacked by at least one other argument
Overview on other options: P. Baroni, M. Caminada and M. Giacomin, An introduction to argumentation semantics

### Beyond abstract argumentation

In the following, we discuss further argumentative notions, argumentation software and algorithms, argumentation schemes and dialogue, and further applications.

**Further argumentative notions**

Abstract argumentation provided the tools to show how several formal reasoning concepts could be interpreted in terms of attacks between arguments.