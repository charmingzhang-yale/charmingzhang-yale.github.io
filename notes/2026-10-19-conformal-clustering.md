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


<blockquote style="background-color: #f0f8f2; color: #394b59; border-left: 4px solid #159957; padding: 12px 18px; border-radius: 0 6px 6px 0;">

  <p><strong style="color: #167d57;">Q1. Why is this approach overly conservative?</strong></p>
  <p>The probability cutoff can overshoot the target. For example, with true cluster probabilities (0.89, 0.11), achieving at least 90% conditional coverage requires including both clusters, yielding 100% coverage but an uninformative set. Unlike conformal prediction's marginal guarantee, this pointwise requirement can be unnecessarily restrictive.</p>

  <p><strong style="color: #167d57;">Q2. Why is it considered non-adaptive?</strong></p>
  <p>Soft labels already vary across observations. What is missing is calibration adaptivity: the cutoff does not use held-out calibration data to adjust for errors in estimated probabilities. If those estimates are inaccurate, nominal coverage is not guaranteed.</p>

</blockquote>

A second possibility is to borrow **split conformal classification**: cluster the training and calibration data, treat the estimated hard labels as ground truth, and calibrate prediction scores accordingly. The difficulty is that these labels are themselves data-dependent. In particular, cluster labels obtained from separately clustered training and calibration sets are not generally exchangeable, undermining the usual conformal coverage guarantee. Treating uncertain assignments as fixed labels can therefore lead to under-coverage.


<blockquote style="background-color: #f0f8f2; color: #394b59; border-left: 4px solid #159957; padding: 12px 18px; border-radius: 0 6px 6px 0;">

  <p><strong style="color: #167d57;">Q3. What does "undermining the usual conformal coverage guarantee" mean?</strong></p>

  
  <p>In standard split conformal classification, observed labels in a held-out calibration set are used to calculate nonconformity scores. Under exchangeability, the resulting prediction set satisfies <strong>P(Y<sub>new</sub> ∈ Ĉ(X<sub>new</sub>)) ≥ 1 − α</strong>.</p>

  <p>For α = 0.1, this means the prediction set contains the true label at least 90% of the time across repeated samples—not necessarily for every individual observation. This is called a <strong>finite-sample marginal coverage guarantee</strong>.</p>

  <p>In clustering, however, true labels are unobserved. Replacing them with estimated hard labels can make calibration and test scores non-exchangeable, since these labels depend on the clustering procedure and potentially on which observations are included. The standard conformal guarantee therefore no longer automatically applies. This does not mean under-coverage is inevitable, only that the theoretical guarantee is lost.</p>

</blockquote>

Together, these limitations motivate an approach that accounts for uncertainty in the cluster labels themselves.

## The Proposed Method: Split Stochastic Conformal Clustering

The key innovation is to replace deterministic cluster assignments with **stochastic labels** sampled from estimated soft clustering probabilities. For example, an observation with probabilities (0.7, 0.2, 0.1) is no longer automatically assigned to Cluster 1; instead, its label is randomly drawn according to these probabilities.

The procedure then follows a split conformal framework. The data are divided into training and calibration sets, each clustered separately to generate stochastic labels. A soft classifier is trained on the training set, while calibration labels are aligned with the classifier's label ordering to account for arbitrary cluster numbering. Finally, conformity scores on the calibration set determine a threshold for constructing confidence sets of plausible labels for new observations.

Rather than treating estimated cluster assignments as ground truth, this approach incorporates their uncertainty into the inference procedure.

<blockquote style="background-color: #f0f8f2; color: #394b59; border-left: 4px solid #159957; padding: 12px 18px; border-radius: 0 6px 6px 0;">

  <p><strong style="color: #167d57;">Q4. Why do we need a soft classifier and label alignment?</strong></p>
  <p>The soft classifier learns to predict cluster membership probabilities from the stochastic training labels. However, cluster numbers are arbitrary: Cluster 1 in the training set might correspond to Cluster 3 in the calibration set. Label alignment finds a permutation that best matches the calibration labels to the classifier's predictions, ensuring that conformal scores compare corresponding clusters rather than mismatched numbers.</p>

  <p><strong style="color: #167d57;">Q5. What exactly does the method output?</strong></p>
  <p>Rather than producing another clustering partition, the method returns a <strong>confidence set of plausible cluster labels</strong> for each query point. For example, Ĉ(x) = {1, 2} indicates that both clusters remain plausible. The statistical goal is to cover the unobserved true label (up to label permutation) with high marginal probability, subject to the method's theoretical assumptions—not to guarantee 90% confidence for every individual observation.</p>

</blockquote>

## Theoretical Guarantees and Empirical Evidence

How reliable are these confidence sets? The main theorem establishes a **finite-sample coverage lower bound** that accounts for two sources of uncertainty: **soft cluster label error**, measuring the discrepancy between estimated and true soft labels, and **replace-one instability**, measuring how much the clustering distribution changes when a single observation is replaced. Rather than claiming unconditional coverage, the framework explicitly quantifies potential under-coverage. Under additional consistency and stability assumptions, the error terms vanish asymptotically, yielding coverage approaching the nominal level. These conditions are verified for a class of correctly specified parametric mixture models.

The empirical results examine both **coverage** and **average confidence set size**. In Gaussian and Gamma mixture simulations, stochastic conformal clustering offers a more favorable balance between reliability and informativeness than the naive approaches in the reported settings. Applications to single-cell RNA-seq further illustrate how confidence sets can reveal ambiguity in cell-type assignments that conventional hard clustering may obscure.







## References

1. Zhang, D., Deng, Y., et al. (2023).
   Spatial epigenome–transcriptome co-profiling of
   mammalian tissues. *Nature*, 616, 113–122.
   https://doi.org/10.1038/s41586-023-05795-1
