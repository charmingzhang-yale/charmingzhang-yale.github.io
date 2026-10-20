---
layout: default
title: "When a Cluster Label Is Not Enough"
permalink: /notes/conformal-clustering/
---

# When a Cluster Label Is Not Enough: Conformal Inference for Clustering

*Research Seminar Notes | Genevera Allen | October 19, 2026*

## Motivation: Why Should We Trust Cluster Assignments?

Clustering is widely used to discover hidden structures in unlabeled data, from identifying cell types in single-cell genomics to uncovering subgroups in complex populations. Yet assigning an observation to a cluster does not necessarily mean that the assignment is reliable. Consider a cell assigned to Cluster 3: could Cluster 2 be equally plausible? Would its assignment change under a different sample or clustering run? Traditional clustering methods often produce definitive labels without directly quantifying such uncertainty. This raises a fundamental statistical question: **How can we construct reliable measures of uncertainty for cluster assignments when the underlying labels are themselves unobserved?**

> **My Reflection — Why This Seminar Caught My Attention**
>
> I was particularly drawn to this seminar because I had recently been struggling to reproduce the clustering results reported by Zhang et al. (2023) in *Nature*. Their analysis of P22 mouse brain data identified 11 RNA clusters, but I could only recover 10 using the released code, with an adjusted Rand index (ARI) of approximately 0.77. I found myself torn between trying to match the published results and questioning whether a closer match necessarily meant a better clustering. After all, the published cluster labels are themselves inferred, not observed ground truth. So what exactly was I trying to reproduce, and how could I tell which clustering was more trustworthy? I came to this seminar hoping to find some new perspectives on that question.
