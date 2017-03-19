---
layout: post
title: "How to Best Serve Micro-tasks to the Crowd when there Is Class Imbalance"
tags: [Crowdsourcing, Class imbalance]
---

<ul id="toc"></ul>

---


# Does class inbalance in relevant judgment affects performance?
We study the effect on crowd worker efficiency and effectiveness of the dominance of one class in the data they process. We aim at understanding if there is any bias in workers seeing many negative examples in the identification of positive labels.
We run comparative experiments where we measure label quality and work efficiency over different class distribution settings both including label frequency (i.e., one dominant class) as well as ordering (e.g., positive cases preceding negative ones).

<img class="wp-image-9418 size-full" src="http://humancomputation.com/blog/wp-content/uploads/2016/10/1.png" alt="batch types" width="80%"/><br> Order of the document classes in each batch, in blue for 'relevant' and red for 'non-relevant'<br>

We used data from TREC8.  To measure effects of class imbalance, we used two different relevant/non-relevant ratios in a batch of judging tasks: 10%-90% and 50%-50%.

## Results
When the relevant documents are shown before the non-relevant ones we obtain the highest precision, while the worst precision is obtained when they are shown at the end of the batch.
Moreover, in batch 2 we observe a low number of true positives and a large number of false positive judgments by the workers, which shows how 90% of non-relevant documents shown at the beginning of the batch create a bias in the workers' notion of relevance.

<img class="size-full wp-image-9427" src="http://humancomputation.com/blog/wp-content/uploads/2016/10/VnamHK01T9yWyS1mlrzj_pic2.png" alt="Mean judgment accuracy, precision and recall for each setting" width="80%"/><br> Mean judgment accuracy, precision and recall for each setting<br>

When classes are balanced, there is no statistically significant difference in the performance between different orders. On the other hand, seeing a similar number of positive and negative documents leads to good performance with more than 60% accuracy in all the three order settings.

## What did we learn?
When most of the documents are non-relevant and the few relevant ones are presented first, workers perform better. This is a positive result which can be easily applied in practice as in real IR evaluation settings most of the documents to be judged are non-relevant.

Including in the first positions documents known to be relevant will both prime workers on relevance as well as allow for training.

While in a real setting it is not possible to put relevant documents first, it would still be possible to order documents by attributes indicating their relevance (e.g., retrieval rank, number of IR systems retrieving the document, etc.) thus presenting first to the workers the documents with higher probability of being relevant.

<em>For more, see our paper, </em><a href="https://arxiv.org/abs/1609.02171">THE EFFECT OF CLASS IMBALANCE AND ORDER ON CROWDSOURCED RELEVANCE JUDGMENTS</a>
<h3 class="title mathjax"><em><small><a href="http://www.dcs.shef.ac.uk/cgi-bin/makeperson?R.Qarout">Rehab K. Qarout</a>, Information School, University of Sheffield</small></em>
<em><small><a href="https://scholar.google.com/citations?user=crhkrNcAAAAJ&amp;hl=en">Alessandro Checco</a>, Information School, University of Sheffield</small></em>
<em><small><a href="https://www.sheffield.ac.uk/is/staff/demartini">Gianluca Demartini</a>, Information School, University of Sheffield</small></em></h3>