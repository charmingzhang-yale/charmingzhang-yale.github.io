---
layout: default
title: "When a Cluster Label Is Not Enough: Conformal Inference for Clustering"
description: "Research Seminar Notes by Charming Zhang"
permalink: /notes/conformal-clustering/
---


<style>
.main-content {
  font-size: 1rem;
  line-height: 1.65;
}
.page-header {
  padding: 2rem 1.25rem;
}
.page-header .project-name {
  font-size: 2rem;
  line-height: 1.3;
}
.page-header .project-tagline {
  font-size: 1rem;
  margin: 0.5rem 0 0;
  opacity: 0.85;
}
@media (max-width: 600px) {
  .page-header .project-name {
    font-size: 1.65rem;
  }
}
</style>

*Seminar: Genevera Allen (Columbia University) · October 19, 2026*

## Motivation: Why Should We Trust Cluster Assignments?

Clustering is widely used to discover hidden structures in unlabeled data, from identifying cell types in single-cell genomics to uncovering subgroups in complex populations. Yet assigning an observation to a cluster does not necessarily mean that the assignment is reliable. Consider a cell assigned to Cluster 3: could Cluster 2 be equally plausible? Would its assignment change under a different sample or clustering run? Traditional clustering methods often produce definitive labels without directly quantifying such uncertainty. This raises a fundamental statistical question: **How can we construct reliable measures of uncertainty for cluster assignments when the underlying labels are themselves unobserved?**

<blockquote style="background-color: #f0f8f2; color: #394b59; border-left: 4px solid #159957; padding: 12px 18px; border-radius: 0 6px 6px 0;">
  <p><strong style="color: #167d57;">My Reflection — Why This Seminar Caught My Attention</strong></p>
  <p>While reproducing the P22 mouse-brain RNA clustering in Zhang et al. (2023), I recovered 10 clusters instead of the reported 11 (ARI ≈ 0.77), even using the released code. I initially wanted to close this gap, but found myself questioning that very goal. If the published cluster labels are themselves inferred rather than observed ground truth, does matching them more closely necessarily mean better clustering? I came to this seminar hoping to find a new perspective on that uncertainty.</p>
</blockquote>

## Why Two Intuitive Approaches Fall Short

A natural first attempt is to use **soft cluster labels** directly. Given estimated cluster probabilities, why not simply include the most likely clusters until their cumulative probability exceeds 1 − α? While intuitive, this approach is limited to clustering methods that provide probabilities for new observations and can produce overly conservative, non-adaptive confidence sets.

A second possibility is to borrow **split conformal classification**: cluster the training and calibration data, treat the estimated hard labels as ground truth, and calibrate prediction scores accordingly. The difficulty is that these labels are themselves data-dependent. In particular, cluster labels obtained from separately clustered training and calibration sets are not generally exchangeable, undermining the usual conformal coverage guarantee. Treating uncertain assignments as fixed labels can therefore lead to under-coverage.

Together, these limitations motivate an approach that accounts for uncertainty in the cluster labels themselves.










## References

1. Zhang, D., Deng, Y., et al. (2023).
   Spatial epigenome–transcriptome co-profiling of
   mammalian tissues. *Nature*, 616, 113–122.
   https://doi.org/10.1038/s41586-023-05795-1
