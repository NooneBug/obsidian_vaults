## Abstract

Argument mining is the automatic identification and extraction of the structure of inference and reasoning expressed as arguments presented in natural language. Understanding argumentative structure makes it possible to determine not only what positions people are adopting, but also why they hold the opinions they do, providing valuable insights in domains as diverse as financial market prediction and public relations. This survey explores the techniques that establish the foundations for argument mining, provides a review of recent advances in argument mining techniques, and discusses the challenges faced in automatically extracting a deeper understanding of reasoning expressed in language in general.

## 1.Introduction

Though data science techniques have been extraordinarily successful in many natural language processing tasks, existing approaches have struggled to identify more complex structural relationships between concepts. For example, although opinion mining and sentiment analysis provide techniques that are proving to be enormously successful in marketing and public relations, and in financial market prediction, with the market for these technologies currently estimated to be worth around $10 billion, they can only tell us what opinions are being expressed and not why people hold the opinions they do.

Justifying opinions by presenting reasons for claims is the domain of argumentation theory, which studies arguments in both text and spoken language; with both normative and empirical methodologies; and from philosophical, linguistic, cognitive and computational perspectives.

Argument analysis aims to turn unstructured text into structured argument data, giving an understanding not just of the individual points being made, but of the relationships between them and how they work together to support (or undermine) the overall message.

Although attempts have been made to increase the speed of manual argument analysis, it is clearly impossible to keep up with the rate of data being generated across even a small subset of areas and, as such, attention is increasingly turning to **argument mining**, the automatic identification and extraction of argument components and structure

Our goal here is to update and extend, introducing reorganization where more recent results suggest different ways of conceptualizing the field. Our intended audience are those already familiar with computational linguistics, so we spend proportionally more time on those parts of the story that may be less familiar to such an audience, and rather less on things that represent mainstays of modern research in computational linguistics.

## 2. Foundational Areas and Techniques

In this section, we look at a range of different areas that constitute precursors to the task of argument mining.

### [[Opinion Mining|2.1 Opinion Mining]]

Opinion mining is “the computational study of opinions, sentiments, and emotions expressed in text” (Liu 2010). The terms “opinion mining” and “sentiment analysis” are often used interchangeably; however, sentiment analysis is specifically limited to positive and negative views, whereas opinion mining may encompass a broader range of opinions

The link between sentiment, opinion, and argumentative structure is described in Hogenboom et al. (2010), where the role that argumentation plays in expressing and promoting an opinion is considered and a framework proposed for incorporating information on argumentation structure into the models for economic sentiment discovery in text.

Based on their role in the argumentation structure, text segments are assigned different weights relating to their contribution to the overall sentiment. Conclusions, for example, are hypothesized to be good summaries of the main message in a text and therefore key indicators of sentiment. The interesting point here, from an argument mining perspective, is that this theory could equally be reversed and sentiment be used as an indicator of the argumentative process found in a text. Taking the example of conclusions, those segments that align with the overall sentiment of the document are more likely to be a conclusion than those that do not.

### 2.2 Controversy Detection 

One extension to the field of opinion mining that has particular relevance to argument mining is controversy detection, where the aim is to identify controversial topics and text where conflicting points of view are being presented. The most clear link between controversy and argument detection can be seen in Boltuziˇ c and ´ Snajder (2015), where ˇ argumentative statements are clustered based on their textual similarity, in order to identify prominent arguments in online debates.

It is easy to see how this process could be reversed, meaning that if we are able to identify controversial points in a piece of text, we already know something about the argumentative structure.

## 3. Manual Argument Analysis

In this section we look at the task of manual argument analysis, considering the steps involved and tools available, as well as the limitations of manually analyzing large volumes of text. Understanding manual analysis can offer unique insight into how this task can be automated and provides a valuable insight into how an analyst unpicks the complex argumentative relationships represented in natural language texts
![[2019_lawrence_fig_1.png]] 

#### 3.1 Text Segmentation 

Text segmentation involves the extraction of the fragments of text from the original piece that will form the constituent parts of the resulting argument structure. Text segmentation can be considered as the identification of a form of elementary discourse units (EDUs). Though there are competing hypotheses about what constitutes an EDU all agree that **EDUs are non-overlapping spans of text corresponding to the atomic units of discourse**. Generally speaking, in argument analysis, the sections that the analyst extracts correspond to the propositions contained within the text; however, some knowledge of the argument being made is often required in order to determine the exact boundaries of these propositions and how fine-grained the segmentation needs to be.

An additional complication can occur in cases where some reconstruction of the argument is required in order to identify the points being made. There is a tendency for arguers to leave implicit an assumption required in order for their conclusion to follow from their premises. This can often occur when the omitted proposition is believed to be obvious; however, it can also happen for a range of other reasons, for example, to increase the rhetorical force of the argument, or to conceal its unsoundness. Such missing premises are referred to as enthymemes (Hitchcock 1985), and can cause difficulties for both automatic and manual segmentation due to the requirement of knowledge that may be outside the scope of that expressed in the text.

#### 3.2 Argument / Non-Argument Classification

This step involves determining which of the segments previously identified are part of the argument being presented and which are not. For most manual analysis tools this step is performed as an integral part of segmentation: The analyst simply avoids segmenting any parts of the text that are not relevant to the argument. However, in some cases, for example, where segmentation has been performed automatically or by a different analyst, this step must be carried out independently.

#### 3.3 Simple Structure

![[2019_lawrence_figure_2.png]]

Once the elements of the argument have been determined, the next step is to examine the links between them. This can be as simple as noting segments that are thematically related, but usually involves the identification of support and attack relations between segments. Although these relations can be simply labeled pairs, it is common to consider the varying ways in which components can work together:

- **Convergent Arguments** In a convergent argument, multiple premises are used to independently support a single conclusion. In this case the premises act on their own and the removal of one premise from the argument does not weaken the others.
- **Linked Arguments** In a linked argument, multiple premises work together to support a conclusion. The important point here is that each premise requires the others in order to work fully.
- **Divergent Arguments** In some cases the same premise may support multiple conclusions. Divergent arguments are somewhat less common and, as such, are not supported by those analysis tools which, for example, are limited to analyzing arguments in a tree structure.
- **Sequential (or Serial) Arguments** The final way in which multiple premises can support a conclusion is in a sequential argument. In this case, one premise leads to another and this, in turn, leads to the conclusion.
- **Rebutting Attacks** Rebutting arguments express a position that is directly incompatible with a conclusion (Pollock 1986, page 38).
- Undercutting Attacks Undercutting arguments attack or conflict with the inference between a premise and a conclusion, and, as such, offer a reason for no longer believing the conclusion, rather than for believing the negation of the conclusion (Pollock 1986, page 39).

Although this approach to identifying argument structure is by far the most common, other methodologies, such as Toulmin (1958) are also widely used; perhaps the clearest synthesis for computational purposes is presented by the philosopher J. B. Freeman (Freeman 1991, 2011). For argument mining, successful extraction of argument structure in one form can often be translated, modulo expressivity constraints, into others (we discuss different argument representations and formats as well as the translation between them in 4).

#### 3.4 Refined Structure

Argumentation schemes are patterns of inference, connecting a set of premises to a conclusion, that represent stereotypical patterns of human reasoning. Such schemes were originally viewed as rhetorical methods by which a speaker could influence their audience; later, they have also been adopted as a way to distinguish good arguments from bad. Arguments are evaluated based on a set of critical questions corresponding to the scheme which, if not answered adequately, result in the argument to which the scheme corresponds defaulting.
![[2019_lawrence_refined_structure.png]]

Experiments on the annotation of Walton schemes by annotators with a strong background in linguistics but who were provided with only the description of the schemes given in Walton, Reed, and Macagno (2008) have shown that this is an exceptionally difficult task, with results differing in both numbers of arguments annotated and the distributions of units (Lindahl, Borin, and Rouces 2019). However, recent developments in annotation guidelines for these schemes, including the decision tree–based method described in Lawrence, Visser, and Reed (2019), suggest that this situation can be improved and offer hope for the construction of scheme annotated corpora.

#### 3.5 Limitations of Manual Analysis

Although these tools can be used for the analysis of small sections of text, analyzing large volumes of text quickly, and certainly in anything approaching real time, is beyond their scope. The major limitation is the amount of information that can be handled by a single analyst

## 5. Argument Mining: Automating Argument Analysis

In this section we now break down the argument mining task into a range of individual challenges (see Figure 3).
![[2019_laurence_fig_3.png]]

Starting from the identification of argument components by segmenting and classifying these as part of the argument being made or not (these tasks are sometimes performed simultaneously, sometimes separated, and sometimes the latter is omitted completely), we move down through levels of increasing complexity: First, considering the role of individual clauses (both intrinsic, such as whether the clause is reported speech, and contextual such as whether the clause is the conclusion to an argument); second, considering argumentative relations from simple premise/conclusion relationships; and third, considering whether a set of clauses forms a complex argumentative relation, such as an instance of an argumentation scheme. A similar classification of argument mining tasks is given in Cabrio and Villata (2018), with Component Detection being split into the subtasks of Boundary Detection and Sentence Classification. Although this represents a robust starting point, it is also important to distinguish the types of classification (argument/nonargument and intrinsic/contextual). Cabrio and Villata also include the broad categorization of Relation Prediction, which again can be further broken down, looking at both general and argumentative relations.

## 6. Identifying Argument Components

The automatic identification of the argumentative sections of a text corresponds to the process of argument/non-argument classification discussed in Section 3.2. Although carrying out this task in isolation does not give us a detailed picture of the argument structure, it has found use in, for example, predicting the usefulness of online reviews based solely on the amount of argumentative text that they contain (Passon et al. 2018).

It is worth noting that the classification of sentences carried out refers only to features intrinsic to the sentence and as such the classification is not robust for sentences that may be part of an argument in one context, but not in a different context.

The idea that the context in which a text span appears can determine whether it is part of an argument or not (Opitz and Frank [2019] have shown that context can be more important than content) can be problematic for the general application of the supervised machine learning approaches discussed so far. In cases where context is not adequately captured, a model trained on one set of data can struggle to classify spans in another set of data where the context is different. As a result, rule-based and unsupervised learning approaches have also been applied to this task.

## 7. Automatic Identification of Clausal Properties

In the previous section we explored a range of techniques for identifying the sections of a text that are argumentative; however, this does not yet tell us anything about the nature of these argumentative text spans, or how they work together. We now move on to look at techniques for automatically identifying properties of argumentative components. In this section, we look at identifying the function of each text span, first considering intrinsic properties (e.g., whether a text span is evidence for a claim) and then look at identifying how a text span is used in the argument as a whole (e.g., premise vs. conclusion).

#### 7.1 Intrinsic Clausal Properties
The first type of clausal properties we look at are those that are intrinsic to the clause itself. Although these properties are limited in what they tell us about the overall argumentative structure, they provide valuable information about the role that a particular text span is playing in the argument as a whole.

#### 7.2 Contextual Clausal Properties
Having considered the argumentative properties intrinsic to a text span, we now move on to look at identifying how a text span is used in the argument as a whole. (it follows a list of approaches)


## 8. Automatic Identification of Relational Properties 
In this section we move on from looking at the identification of clausal properties to the identification of inter-clausal relations. We look first at general argumentative relations, for example, premise/conclusion relationships, and then move on to look at the more complex relationships involved in argumentation schemes and dialogical relations.

#### 8.1 Identifying General Argumentative Relations
Identifying relations between pairs of propositions is a more complex and nuanced task than identifying the roles that an individual proposition may take. It is one thing to know, for example, that a given proposition is a premise; much more challenging is to determine also for which conclusion (or conclusions) it serves as premise. Approaches to identifying these relations either build upon the prior classification of individual clauses, or aim to extract relations directly.

#### 8.2 Identifying Complex Argumentative Relations 
The ability to successfully extract premises and conclusions is built upon in Feng and Hirst (2011), which presents the first step in the long-term goal of a method to reconstruct enthymemes, by first, classifying to an argumentation scheme (Walton, Reed, and Macagno 2008), then fitting the propositions to the template, and finally, inferring the enthymemes.

## 9. Conclusion 
The recent rapid growth in argument mining shows that there is an increasing demand for the automated extraction of deeper meaning from the vast amounts of data that we currently produce. Although techniques in opinion mining are able to tell us what people are thinking, we also need to be able to say why they hold those opinions. There is substantial commercial opportunity here as businesses increasingly want to build on the data that they gather in order to know more about the thoughts and behaviors of their customers, and it is unsurprising that many of the large players in the field are engaging, most visibly to date, IBM.

One of the first challenges faced by argument mining is the lack of consistently annotated argument data. Much recent work has focused on producing annotation guidelines targeted at specific domains (e.g., Kirscgner, Eckle-Kohler, and Gurevych 2015; Walker, Vazirova, and Sanford 2014; Kiesel et al. 2015), and although this has shown that data from these fields can be consistently annotated, the use of specific annotation schemes aimed at individual areas means that any techniques developed using these data are limited to that domain. The volume of data, particularly data annotated at the most fine grained level, is still far below what would be required to apply many of the techniques previously discussed in a domain independent manner. Attempts are being made to overcome this lack of data, including the use of crowdsourced annotation (Ghosh et al. 2014; Skeppstedt, Peldszus, and Stede 2018) and automatic methods to extend the data currently annotated (Bilu, Hershcovich, and Slonim 2015). As these efforts combine with increasing attention to manual analysis, the volume of data available should increase rapidly. Schulz et al. (2018) also offer some solace in this regard, showing how multi-task learning (training models across data sets from different domains) can improve results in domains where limited domain specific annotated data is available. Even in cases where there is a greater volume of data, conflicting notions of argument are often problematic. In a qualitative analysis of six different, widely used, argument data sets, Daxenberger et al. (2017) show that each data set appears to conceptualize claims quite differently. These results clearly highlight the need for greater effort in building a framework in which argument mining tasks are carried out, covering all aspects from agreement on the argument theoretical concepts being identified, through to uniform presentation of results and data A related problem is verifiability and reproducibility of results: As a young field, argument mining does not yet benefit from uniformly publicly available algorithms and codebases that would encourage incremental advance. Initiatives such as CLARIN (Krauwer and Hinrichs 2014) and LAPPSGrid (Ide et al. 2015) are trying to tackle this challenge across NLP, and argument technologies might be expected to contribute to, and benefit from, these initiatives in much the same way that other specialities within NLP can. Beyond these logistical and theoretical issues, there also remains the fact that argument mining is a difficult task; as Moens (2018) points out, “a lot of content is not expressed explicitly but resides in the mind of communicator and audience.” It seems that to overcome this challenge we need to look at the broader picture in which argument occurs. In this regard, works that either take a more holistic “end-to-end” view (Stab and Gurevych 2017; Persing and Ng 2016; Potash, Romanov, and Rumshisky 2017) or that aim to harness external data sources (Rinott et al. 2015; Lawrence and Reed 2017) seem to point the way. Argument mining techniques have been successfully developed to extract details of the argumentative structure expressed within a piece of text, focusing on different levels of argumentative complexity as the domain and task require. For each task, we have considered work carried out using a broad range of techniques, including statistical and linguistic methods. We have presented a hierarchy of task types based on increasing argumentative complexity. First looking at the identification of argument components and the determination of their boundaries, we have then moved on to consider the role of individual clauses (both intrinsic, such as whether the clause is reported speech, and contextual, such as whether the clause is the conclusion to an argument). Finally, we have considered the identification of a range of argumentative relations from simple premise/conclusion relationships, to whether a set of clauses form an instance of an argumentation scheme. The success of these techniques and the development of techniques for analyzing dialogical argument offers hope that techniques can be developed for automatically identifying complex illocutionary structures and the argumentative structures they build. We have also seen how these techniques can be combined, tying together statistical identification of basic structure and linguistic markers and identifying scheme components. In so doing, the resulting argument structures offer a more complete analysis of the text than any of these methods provide on their own. Argument mining remains profoundly challenging, and traditional methods on their own seem to need to be complemented by stronger, knowledge-driven analysis and processing. However, the pieces required to successfully automate the process of turning unstructured data into structured argument are starting to take shape. As the volume of analyzed argument continues to increase, and existing techniques are further developed and brought together, rapid progress can be expected.