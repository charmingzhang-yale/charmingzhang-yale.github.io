---
layout: default
title: "When a Cluster Label Is Not Enough"
permalink: /notes/conformal-clustering/
---

# When a Cluster Label Is Not Enough: Conformal Inference for Clustering

*Research Seminar Notes | Genevera Allen | October 19, 2026*

## Motivation: Why Should We Trust Cluster Assignments?

Clustering is widely used to discover hidden structures in unlabeled data, from identifying cell types in single-cell genomics to uncovering subgroups in complex populations. Yet assigning an observation to a cluster does not necessarily mean that the assignment is reliable. Consider a cell assigned to Cluster 3: could Cluster 2 be equally plausible? Would its assignment change under a different sample or clustering run? Traditional clustering methods often produce definitive labels without directly quantifying such uncertainty. This raises a fundamental statistical question: **How can we construct reliable measures of uncertainty for cluster assignments when the underlying labels are themselves unobserved?**
