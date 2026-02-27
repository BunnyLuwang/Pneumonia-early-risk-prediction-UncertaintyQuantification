# Reliability-Aware Early Radiographic Progression Modeling

## Overview
This project develops a reliability-aware deep learning framework for early radiographic severity progression modeling using chest X-rays.

The work focuses on:
- Temporal early-risk modeling
- Calibration analysis
- Epistemic uncertainty estimation (MC Dropout)
- Selective prediction
- Distribution shift stress testing
- Latent state progression analysis (digital twin prototype)

## Dataset
RSNA Pneumonia Detection Challenge Dataset (Kaggle)

## Methods
- ResNet-based CNN
- Severity-based temporal simulation
- Expected Calibration Error (ECE)
- Monte Carlo Dropout
- Selective prediction under abstention
- Latent state manifold analysis

## Key Results
- Temporal AUROC: ~0.82
- Meaningful uncertainty–error separation
- Uncertainty degradation under distribution shift
- Strong correlation (r ≈ 0.88) between latent progression axis and predicted risk
