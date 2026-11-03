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




