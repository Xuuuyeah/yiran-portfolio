---
title: "Parkinson's Freezing of Gait Prediction"
date: 2023-06-01T12:00:00+00:00
image: "images/portfolio/item5.jpg"
categories: ["deep-learning","data-science"]
description: "1D-CNN model for detecting freezing of gait events in Parkinson's patients using wearable sensor data. Kaggle Silver Medal."
draft: false
external_url: "https://www.kaggle.com/competitions/tlvmc-parkinsons-freezing-gait-prediction/overview"
project_info:
- name: "Tech Stack"
  icon: "fas fa-layer-group"
  content: "Python, PyTorch, NumPy, SciPy, Pandas"
- name: "Architecture"
  icon: "fas fa-project-diagram"
  content: "1D-CNN with Focal Loss & Signal Processing"
- name: "Competition"
  icon: "fas fa-trophy"
  content: "[Kaggle Competition Page](https://www.kaggle.com/competitions/tlvmc-parkinsons-freezing-gait-prediction)"
- name: "Achievement"
  icon: "fas fa-medal"
  content: "Kaggle Silver Medal"
---

Built a 1D Convolutional Neural Network to detect freezing of gait (FOG) events in Parkinson's disease patients from wearable accelerometer data, achieving a **Kaggle Silver Medal** in the TLVMC Parkinson's Freezing of Gait Prediction competition.

#### Data & Signal Processing

The competition dataset includes 3-axis accelerometer signals from lower-back sensors, with three target event types: **Start Hesitation**, **Turn**, and **Walking**.

<img src="/images/portfolio/fog_data_preview.png" alt="FOG Dataset Preview" class="img-fluid mb-4">

- Applied **Butterworth high-pass and low-pass filters** to isolate relevant frequency bands from raw accelerometer signals
- Computed **spectrograms** via Short-Time Fourier Transform (STFT) to capture time-frequency features
- Engineered window-based features with `window_size=200` and `window_future=75` samples for temporal context

#### Model Architecture

Designed a 1D-CNN with progressively deeper feature extraction:

- **4 Convolutional Blocks** — Channel progression [32 → 64 → 64 → 128], each with BatchNorm, ReLU, MaxPool, and Dropout
- **Focal Loss** (γ=2.0) to handle severe class imbalance across FOG event types
- **Dual-protocol training** — Separate models for `tdcsfog` (lab-based) and `defog` (at-home) data protocols to account for different sensor configurations
- **6-fold Cross-Validation** for robust model selection and ensemble predictions

#### Training Strategy

- Trained with AdamW optimizer and OneCycleLR scheduler (max_lr=5e-4)
- Applied per-protocol normalization using dataset-specific statistics
- Ensemble of 6 CV folds for final predictions, averaging logits across folds

#### Results

- **Kaggle Silver Medal** in the competition with 1,379 teams
- Model effectively distinguishes between Start Hesitation, Turn, and Walking events in real-time sensor streams
- Dual-protocol approach improved generalization across lab and home recording settings
