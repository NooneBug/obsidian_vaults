https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=7817097

"This paper addresses the task of assigning multiple labels of fine-grained named entity (NE) types to Wikipedia articles. To address the sparseness of the input feature space, which is salient particularly in fine-grained type classification, we propose to learn article vectors (i.e. entity embeddings) from hypertext structure of Wikipedia using a Skip-gram model and incorporate them into the input feature set. To conduct large-scale practical experiments, we created a new dataset containing over 22,000 manually labeled instances."

Contributions:
---

• We propose to encode the local context of hyperlinks as vectors using the Skip-gram model. We make the obtained vectors publicly available1. 
• We created a new dataset by manually annotating over 22,000 Japanese Wikipedia articles with fine-grained NE types. The dataset is available if one contacts the authors. 
• We tested our model on our new dataset and empirically showed its positive impacts on the accuracy of classification.


Method:
---

To obtain article embedding, first, we replace every anchor text with the title of the article referred to by the hyperlink of the anchor text. Next, we assume all occurrences of the phrase identical to an anchor text to have hyperlinks to the article linked by the anchor text. This is based on the one-sense per-discourse assumption. In addition, all white spaces in article titles are replaced with “_” to prevent article titles from being separated into words. In this way, we jointly learn vectors of words and articles. We use word2vec to obtain 200 dimensional vectors.

Then a binary classifier for each wikipedia category is trained on top of the encoder

---
Masatoshi Suzuki∗, Koji Matsuda∗, Satoshi Sekine†, Naoaki Okazaki∗ and Kentaro Inui∗

∗ Tohoku University
† Language Craft Inc.

#paper 