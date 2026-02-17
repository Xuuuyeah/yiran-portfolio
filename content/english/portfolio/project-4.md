---
title: "Stiff Person Syndrome Risk Prediction with Deep Learning"
date: 2025-12-01T12:00:00+00:00
image: "images/portfolio/item4.jpg"
categories: ["deep-learning","research"]
description: "Transformer-based RiskNet model for early prediction of Stiff Person Syndrome from longitudinal medical claims data."
draft: false
project_info:
- name: "Tech Stack"
  icon: "fas fa-layer-group"
  content: "Python, TensorFlow/Keras, XGBoost, Altair, Polars, Hydra"
- name: "Architecture"
  icon: "fas fa-project-diagram"
  content: "Transformer-based RiskNet with Age-Conditioned Embeddings"
- name: "Poster"
  icon: "fas fa-file-pdf"
  content: "[ASHP Poster (PDF)](/ASHP_Poster_SPS.pdf)"
- name: "Domain"
  icon: "fas fa-heartbeat"
  content: "Healthcare AI & Rare Disease Prediction"
---

Developed a Transformer-based deep learning model (**RiskNet**) to predict Stiff Person Syndrome (SPS) risk from longitudinal patient medical claims data, enabling early screening for this rare neurological disorder.

#### Model Architecture

Built a multi-horizon prediction model using a custom Transformer architecture:

- **Age-Conditioned Embeddings** — Token embeddings (128-dim) modulated by cosine-based temporal encoding to capture disease evolution over time
- **4-layer Transformer Encoder** — 6 attention heads per block with residual connections, layer normalization, and dropout (0.2)
- **Cumulative Probability Layer** — Outputs risk predictions at 5 time horizons (3, 6, 12, 24, 36 months before diagnosis)
- **Focal Loss** (α=0.25, γ=2.0) to handle extreme class imbalance (~3% positive rate)

#### Model Performance

The model achieved strong predictive performance on held-out test data:

<img src="/images/portfolio/sps_roc_prc.png" alt="ROC and Precision-Recall Curves" class="img-fluid mb-4">

- **AUROC = 0.92** on the 60-month prediction window
- **AUPRC = 0.66** — significantly above the 0.089 baseline for imbalanced data
- Performance remained stable across lower prevalence thresholds, supporting robustness

#### Feature Importance via Integrated Gradients

Integrated Gradients attribution analysis on the Transformer model identified the most predictive ICD-10 diagnosis codes across 6,144 patients:

<img src="/images/portfolio/sps_ig_top15.png" alt="Top 15 Predictive ICD-10 Codes via Integrated Gradients" class="img-fluid mb-4">

- **Hypertension (I10)** and **low back pain (M545)** emerged as the strongest predictive signals
- Neurological indicators (**tremor, polyneuropathy**) and psychiatric comorbidities (**bipolar disorder**) are clinically consistent with SPS presentation
- **Muscle spasm (M6283)** — a hallmark SPS symptom — also ranks among the top predictive codes

#### Clinical Impact

- Multi-horizon predictions enable risk-stratified patient screening at different time points
- Explainable AI outputs help clinicians understand which medical history patterns signal SPS risk
- Early recognition of symptom patterns could reduce diagnostic delay and healthcare burden
