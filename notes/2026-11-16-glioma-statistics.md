---
layout: default
title: "From Molecular Subtypes to Clinical Decisions: Statistics in Glioma Care"
description: "Research Seminar Notes"
permalink: /notes/glioma-statistics/
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

*Speaker: Prof. Annette Molinaro · University of California, San Francisco · November 16, 2026*

*Talk: The Role of Statistics in Changing Glioma Patient Care*

## Motivation: When Does a Biological Classification Become Clinically Useful?


Classifying tumors is not simply a matter of dividing patients into distinct groups. A classification may reflect meaningful biological differences, but how can we determine whether those differences are also relevant to clinical outcomes? This question is particularly important for gliomas, where tumors that appear similar under conventional histological classification may differ substantially in their molecular characteristics and prognosis.

One example is the molecular classification developed by Eckel-Passow, Molinaro, and colleagues [1]. Using three established molecular alterations—IDH mutations, TERT promoter mutations, and 1p/19q codeletion—the researchers defined five major glioma groups among 1,087 patients. These groups differed in age at diagnosis, genetic characteristics, and overall survival. However, their prognostic associations were not uniform: molecular group remained independently associated with survival among grade II–III gliomas after adjustment for clinical factors, but not among grade IV gliomas.

Rather than assuming that a biologically meaningful classification is automatically clinically useful, this example illustrates how statistical analysis can evaluate where molecular distinctions provide relevant prognostic information, and where their value may depend on the patient population.


<blockquote style="background-color: #f0f8f2; color: #394b59; border-left: 4px solid #159957; padding: 12px 18px; border-radius: 0 6px 6px 0;">

  <p><strong style="color: #167d57;">My Reflection — Knowledge-Driven vs. Data-Driven Classification</strong></p>

  <p>I do not think knowledge-driven classification and data-driven clustering can be easily ranked by which is more valuable. Ideally, I would hope that structures discovered through statistical methods could corroborate existing, biologically interpretable classifications, allowing the two approaches to reinforce each other. Yet I realize that such agreement may be too idealistic, and it should not be the only measure of success.</p>

  <p>Relying too heavily on established biological classifications may limit our ability to discover something genuinely new, while judging clustering solely by statistical metrics may overlook its biological meaning. Looking back, I feel that my thinking during the previous seminars sometimes leaned more toward the data and methodological side. This seminar offered a valuable complementary perspective, encouraging me to consider biological interpretation and clinical relevance when evaluating a classification.</p>

</blockquote>


## From Molecular Subtypes to Prognostic Models

Identifying biologically distinct tumor groups is only the beginning. To evaluate their prognostic value, we need to ask whether these distinctions help explain differences in patient survival. Unlike ordinary regression outcomes, survival data often involve censoring, as some patients remain alive at the end of follow-up. Kaplan–Meier curves can describe survival differences across groups, while Cox proportional hazards models examine associations after adjusting for clinical factors such as age and tumor grade.

But what if the relationships between these predictors and survival are more complicated than a conventional Cox model can adequately capture? In a study of newly diagnosed glioblastoma, Molinaro and colleagues [2] examined survival in relation to molecular status, patient characteristics, and extent of surgical resection. Because the proportional hazards assumption was not satisfied for some predictors, particularly extent of resection, the researchers also used **recursive partitioning** to identify patient groups with different survival experiences. These risk groups were subsequently evaluated in independent cohorts, illustrating how statistical models can help translate complex prognostic associations into more interpretable patient stratification.

An important distinction remains between **statistical association and predictive improvement**. A molecular marker may remain significantly associated with survival after adjustment for other variables, yet contribute little to a model's ability to distinguish patients with different risks. Measures such as the **C-index** assess predictive discrimination, while calibration examines whether predicted survival probabilities agree with observed outcomes. Establishing prognostic relevance therefore requires more than identifying statistically significant regression coefficients, especially when new biomarkers are being added to models that already contain strong clinical predictors.


## Beyond Tumor Genetics: High-Dimensional Biomarkers

Molecular classification provides important prognostic information, but patients within the same molecular subtype can still experience substantially different outcomes. Could other biological measurements help explain this remaining variation? Two studies presented in the seminar explored this question using high-dimensional DNA methylation data and digital pathology images.

In the first study, Molinaro and colleagues [3] used blood DNA methylation profiles to estimate immune cell proportions and epigenetic age. Rather than treating individual methylation sites as separate predictors, the researchers applied reference-based cell mixture deconvolution to obtain biologically interpretable immune characteristics. They then used survival analysis and recursive partitioning to investigate how these characteristics interacted with patient age. Among 197 patients in the training set, combinations of age, CD4+ T-cell proportion, and neutrophil proportion identified four groups with markedly different survival outcomes. Similar risk stratification was subsequently examined in 350 patients with other glioma molecular subtypes.

A different approach was explored by Chunduru, Phillips, and Molinaro [4], who developed a **survival deep learning** framework using H&E-stained digital pathology images from 766 glioma patients. A convolutional neural network learned image-based risk scores using survival outcomes, while Cox regression assessed their prognostic value beyond existing clinical and molecular characteristics. Adding the learned risk score to a model containing age and molecular subtype increased the reported C-index from 0.82 to 0.84.

These studies illustrate two ways of extracting prognostic information from high-dimensional data: one uses biological reference knowledge to construct interpretable features, while the other learns representations directly from images. Yet **statistical association, improved prediction, and biological interpretation are distinct achievements**. A complex representation may contain useful information beyond established markers, but its predictive improvement must be evaluated carefully, and its clinical relevance requires further validation.


## From Prognosis to Treatment Decisions

A biomarker may help predict how long a patient is likely to survive, but does that tell us which treatment would benefit the patient most? Not necessarily. **Prognostic prediction** concerns the likelihood of future outcomes, whereas **causal inference** asks how those outcomes might change under different interventions. A patient with a poor prognosis does not necessarily benefit more from aggressive treatment, and a strong predictor of survival is not automatically a predictor of treatment benefit.

This distinction is particularly important when studying the **extent of surgical resection (EOR)** in glioma patients. Observational studies may find that patients who undergo more extensive tumor removal survive longer. However, the extent of resection is not randomly assigned: tumor location, preoperative tumor volume, and patient characteristics may influence both surgical decisions and subsequent survival. These differences introduce potential confounding, making it difficult to interpret observed survival differences as causal effects of surgery.

In a study of 757 patients with IDH-mutant grade 2 glioma, Hervey-Jumper and colleagues [5] used **propensity score matching** to compare patients with similar observed characteristics but different extents of resection. Their analysis found that EOR of at least 75% was associated with improved overall survival, while a threshold of 80% was reported for progression-free survival. By accounting for measured differences between patients, propensity score methods can make observational comparisons more informative. Nevertheless, they cannot eliminate unmeasured confounding or fully reproduce randomized treatment assignment.

Even with stronger evidence of treatment benefit, clinical decisions require more than survival estimates alone. More extensive surgery may improve tumor control while increasing the risk of neurological impairment. Translating statistical evidence into patient care therefore requires considering **expected treatment benefit, potential harm, and individual patient circumstances**, rather than relying on any single prognostic marker or predicted outcome.

<blockquote style="background-color: #f0f8f2; color: #394b59; border-left: 4px solid #159957; padding: 12px 18px; border-radius: 0 6px 6px 0;">

  <p><strong style="color: #167d57;">My Reflection — From Prognostic Value to Clinical Decisions</strong></p>

  <p>I think a biomarker that predicts mortality risk can still have clinical value, even if it cannot tell us which treatment would be most effective. It can help us understand a patient's prognosis and serve as a useful reference when planning care, but it should not determine treatment decisions on its own. For glioma surgery in particular, deciding whether more extensive resection is worthwhile requires evidence about potential survival benefits, surgical risks, and possible neurological damage, as well as the clinician's judgment about the individual patient. This made me realize that <strong>predicting what may happen to a patient and determining how to intervene for a better outcome are two different statistical questions</strong>.</p>

</blockquote>


## From Statistical Evidence to Clinical Impact

A statistical model may identify meaningful patient subgroups or predict survival with reasonable accuracy, but how can we know whether its findings will remain reliable beyond the original study population? Internal validation can assess model performance within the available data, yet it cannot fully capture differences in patient characteristics, clinical practices, or measurement procedures across institutions.

**External validation** provides an important next step. In the glioblastoma study by Molinaro and colleagues [2], prognostic risk groups developed at UCSF were evaluated using independent patient cohorts from the Mayo Clinic and the Ohio Brain Tumor Study. Similarly, Hervey-Jumper and colleagues [5] examined the reproducibility of survival risk stratification in two external cohorts. Such analyses help establish whether statistical findings extend beyond the populations in which they were originally developed. For models that estimate individual survival probabilities, evaluation should also consider **discrimination and calibration**, rather than relying on risk separation alone [6].

Yet successful external validation does not automatically establish clinical benefit. Even if a model reliably predicts patient outcomes, we still need to determine whether using its predictions would lead to better treatment decisions. Measures of clinical utility, such as net benefit, can help evaluate potential decision consequences, while evidence of actual clinical impact requires studying what happens when the model is introduced into practice.

The broader challenge is therefore not simply to discover statistically meaningful patterns, but to understand **which conclusions those patterns support, how reliably they generalize, and whether acting on them can improve patient care**.


## References

[1] Eckel-Passow, J. E., Lachance, D. H., Molinaro, A. M., et al. (2015). Glioma Groups Based on 1p/19q, IDH, and TERT Promoter Mutations in Tumors. *New England Journal of Medicine*, 372, 2499–2508. [https://doi.org/10.1056/NEJMoa1407279](https://doi.org/10.1056/NEJMoa1407279)


[2] Molinaro, A. M., Hervey-Jumper, S., Morshed, R. A., et al. (2020). Association of Maximal Extent of Resection of Contrast-Enhanced and Non–Contrast-Enhanced Tumor With Survival Within Molecular Subgroups of Patients With Newly Diagnosed Glioblastoma. *JAMA Oncology*, 6(4), 495–503. [https://doi.org/10.1001/jamaoncol.2019.6143](https://doi.org/10.1001/jamaoncol.2019.6143)


[3] Molinaro, A. M., Wiencke, J. K., Warrier, G., et al. (2022). Interactions of Age and Blood Immune Factors and Noninvasive Prediction of Glioma Survival. *Journal of the National Cancer Institute*, 114(3), 446–457. [https://doi.org/10.1093/jnci/djab195](https://doi.org/10.1093/jnci/djab195)

[4] Chunduru, P., Phillips, J. J., & Molinaro, A. M. (2022). Prognostic Risk Stratification of Gliomas Using Deep Learning in Digital Pathology Images. *Neuro-Oncology Advances*, 4(1), vdac111. [https://doi.org/10.1093/noajnl/vdac111](https://doi.org/10.1093/noajnl/vdac111)

[5] Hervey-Jumper, S. L., Zhang, Y., Phillips, J. J., et al. (2023). Interactive Effects of Molecular, Therapeutic, and Patient Factors on Outcome of Diffuse Low-Grade Glioma. *Journal of Clinical Oncology*, 41(11), 2029–2042. [https://doi.org/10.1200/JCO.21.02929](https://doi.org/10.1200/JCO.21.02929)

[6] Riley, R. D., Archer, L., Snell, K. I. E., et al. (2024). Evaluation of clinical prediction models (part 2): How to undertake an external validation study. *BMJ*, 384, e074820. [https://doi.org/10.1136/bmj-2023-074820](https://doi.org/10.1136/bmj-2023-074820)




