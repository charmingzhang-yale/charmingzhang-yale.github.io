---
layout: default
title: "When Models Age: Statistical Perspectives on Durable Clinical AI"
description: "Research Seminar Notes"
permalink: /notes/durable-clinical-ai/
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

*Speaker: Prof. Tianxi Cai · Harvard T.H. Chan School of Public Health · November 2, 2026*

*Talk: From Real-World Data to Durable Clinical AI: Building Reliable Evidence Across Institutions and Over Time*

## Motivation: What Happens After Model Deployment?

Statistical models are typically developed and evaluated using data collected within a particular period. Yet a model that performs well today may not remain reliable years after deployment. Patient populations, clinical practices, coding systems, and treatment options can all change, potentially altering both the distribution of predictors and their relationships with clinical outcomes.

This problem is particularly consequential for clinical AI, where models may continue to inform real-world decisions long after their initial validation. Temporal and institutional distribution shifts can gradually undermine predictive performance, while limited outcome labels, computational costs, and regulatory constraints make frequent retraining difficult.

In this seminar, Tianxi Cai presented a broader perspective on clinical AI: rather than focusing solely on predictive accuracy at the time of development, statistical methods should also address how models can remain reliable across changing environments.


<blockquote style="background-color: #f0f8f2; color: #394b59; border-left: 4px solid #159957; padding: 12px 18px; border-radius: 0 6px 6px 0;">

  <p><strong style="color: #167d57;">My Reflection — Time in the Data vs. Time After Deployment</strong></p>

  <p>I have worked with several time series models and have often thought about how time affects the data being modeled. What I had rarely considered, however, was what happens to the model itself as time passes. Looking back, I realize that I had often treated model fitting and validation as the end of an analysis, without asking whether the same model would remain reliable years later.</p>

  <p>This seminar made me reconsider that assumption. Even if a model accounts for temporal patterns in its training data, will its predictions remain trustworthy when the population and environment have changed? My first instinct would be to collect new data and retrain the model, but I had not seriously considered how difficult that might be in real clinical settings.</p>

</blockquote>

## From EHR Data to Reliable Evidence

Electronic health records (EHRs) contain extensive clinical information, but how much of it can be treated as reliable evidence? Diagnostic codes do not always correspond to confirmed diseases, while important clinical outcomes may remain buried in unstructured notes. In one example presented during the seminar, only 58% of patients with three or more rheumatoid arthritis codes actually had the disease. Having more data, therefore, does not necessarily mean having more accurate clinical labels.

One way to address this problem is to extract and organize information that conventional structured records may miss. The seminar presented **representation learning and knowledge graphs** for integrating heterogeneous EHR data, alongside **large language models (LLMs)** for extracting clinical information from free-text notes. In a human–agent co-learning example, the reported annotation accuracy improved from 81.4% to 89.0% through a process involving human review and model refinement.

Yet an automatically generated annotation is not equivalent to an observed clinical outcome. Even if LLMs make it possible to label thousands of additional records, those labels may still contain errors. Treating them as ground truth could carry these errors into downstream prediction or statistical inference. The challenge is therefore not only to obtain clinical information at scale, but also to account for its reliability.

## GUARD: Updating Models Under Distribution Shift

When a prediction model deteriorates over time, a natural response is to retrain it using more recent data. But what if reliable outcome labels are scarce, or frequent retraining is too costly? One alternative is **transfer learning**, which borrows information from historical or external populations. However, conventional approaches often favor sources that closely resemble the current target population, potentially overlooking useful information from more heterogeneous sources.

Another approach is **distributionally robust optimization (DRO)**, which seeks a model that performs well under unfavorable distributions within a specified uncertainty set. While this offers protection against distribution shifts, an overly broad uncertainty set can lead to conservative predictions that sacrifice accuracy in the current population. This creates a tension between **optimizing for today's patients and preparing for tomorrow's uncertainty**.

To address this trade-off, **GUARD (Guided and Uncertainty-Aware Robustness to Domain Shift)** combines target-guided transfer learning with robust optimization [1]. Rather than retraining a complex model from scratch, it constructs a lower-dimensional update using the existing predictor and additional features. Its central idea is to borrow information from mixtures of heterogeneous source populations while remaining anchored to the current target. Importantly, GUARD also accounts for differences in the statistical uncertainty of source estimates, rather than treating every source as equally reliable. Double machine learning and cross-fitting are used to support efficient estimation and inference.

In an application to rheumatoid arthritis disease activity prediction, GUARD maintained relatively stable prediction errors across subsequent years, while several conventional approaches experienced greater performance degradation. The results illustrate why evaluating a model only at the time of development may miss an important dimension of its reliability: how well it continues to perform as the clinical environment changes.


<blockquote style="background-color: #f0f8f2; color: #394b59; border-left: 4px solid #159957; padding: 12px 18px; border-radius: 0 6px 6px 0;">

  <p><strong style="color: #167d57;">Q2. How much present accuracy should we sacrifice for future robustness?</strong></p>

  <p>My instinct is to accept some loss in current predictive accuracy if it makes a model more reliable over time. But how much should we be willing to sacrifice? I find it difficult to decide where that balance should lie, especially when future distribution shifts are unknown. Even if we can quantify the trade-off statistically, I wonder whether the appropriate choice ultimately depends on the clinical consequences of prediction errors.</p>

</blockquote>



## References

[1] Xiong, X., Guo, Z., & Cai, T. (2026). Guided Uncertainty-Aware Robust Domain Transfer. *arXiv preprint*, arXiv:2609.35654. [https://doi.org/10.48550/arXiv.2609.35654](https://doi.org/10.48550/arXiv.2609.35654)

[2] Gu, Y., Liao, K., & Cai, T. (2026). Unveiling Invariant and Transferable Latent Factors Across Heterogeneous Environments via ATLAS. *arXiv preprint*, arXiv:2607.18209. [https://doi.org/10.48550/arXiv.2607.18209](https://doi.org/10.48550/arXiv.2607.18209)



