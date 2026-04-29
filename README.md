# Reliability-Aware Early Radiographic Progression Modeling

## Overview

This project develops a **reliability-aware deep learning framework** for disease severity prediction and progression modeling from chest X-rays using the RSNA Pneumonia Detection dataset.

Rather than focusing only on classification accuracy, this work systematically investigates:

- Model calibration
- Uncertainty estimation
- Reliability under distribution shift
- Temporal progression modeling (simulated)
- Latent representation structure

The project is structured in **progressive phases**, each increasing task difficulty and analytical depth.

---

## Project Structure

### Phase 1 — Baseline Severe Risk Prediction
- Task: Predict severe vs non-severe cases (including normal images)
- Model: ResNet-based CNN
- Focus:
  - AUROC, Brier score
  - Calibration (ECE, reliability diagrams)
  - Uncertainty estimation (MC Dropout)

**Key Insight:**
Uncertainty strongly correlates with prediction errors in simpler classification settings.

---

### Phase 2 — Pneumonia Severity Discrimination
- Task: Distinguish **mild vs severe pneumonia only** (normal cases removed)
- Increased task difficulty

**Findings:**
- Lower AUROC compared to Phase 1  
- Worse calibration  
- Reduced uncertainty–error separation  

**Insight:**
Model reliability degrades as task difficulty increases.

---

### Phase 3 — Reliability & Distribution Shift Analysis

#### Uncertainty & Selective Prediction
- Monte Carlo Dropout used for epistemic uncertainty
- Selective prediction applied:
  - Abstain on high-uncertainty samples
  - Improves accuracy at lower coverage

#### Distribution Shift (Severity-Based)
- Train on moderate severity cases  
- Test on extreme severity cases  

**Findings:**
- Discrimination may improve under shift  
- But **uncertainty–error relationship degrades**

**Insight:**
Uncertainty is not always reliable under distribution shift.

---

### Phase 4 — Temporal Early Progression Modeling

Since real temporal data is unavailable, temporal structure is simulated:

- Compute severity score from bounding boxes
- Split pneumonia cases:
  - Bottom 40% → Early state  
  - Top 40% → Future severe state  
- Middle 20% removed to reduce ambiguity  

Task:
> Predict progression from early state to future severe state

**Results:**
- Temporal AUROC: ~0.82  
- Moderate calibration error (ECE ~0.15)  
- Uncertainty still correlates with errors (~2× difference)  
- Selective prediction improves performance  

**Insight:**
Temporal progression modeling behaves differently from static classification but still benefits from uncertainty estimation.

---

## Latent State Analysis (Digital Twin Interpretation)

- Extracted 512-dimensional embeddings from CNN
- Defined progression direction:

  d = μ_future − μ_early

- Projected each sample onto this axis

**Findings:**
- Clear separation between early and severe states  
- Strong correlation between projection and predicted risk:

  **r ≈ 0.88**

**Interpretation:**
The model learns a **continuous disease progression structure in latent space**, supporting a minimal **latent-state transition (digital twin–like) interpretation**.

---

## Methods Summary

- ResNet-based CNN
- Severity-based temporal simulation
- Monte Carlo Dropout (epistemic uncertainty)
- Expected Calibration Error (ECE)
- Selective prediction (coverage vs accuracy)
- Covariate shift stress testing
- Latent embedding analysis (PCA + projection)

---

## Dataset Notes

- Bounding box fields (`x, y, width, height`) contain NaNs for normal cases  
- NaNs indicate **absence of pneumonia**, not missing data  
- Severity computed as total bounding box area per image  

---

## Key Takeaways

- Model reliability depends strongly on task difficulty  
- Uncertainty is useful in-distribution but may fail under shift  
- Temporal progression can be approximated via severity stratification  
- Deep models learn structured latent progression representations  

---

## Limitations

- Temporal structure is simulated (no real longitudinal data)  
- Single-step progression prediction  
- No intervention modeling  
- No patient-level longitudinal tracking  

---

## Future Work

- Apply to longitudinal datasets (e.g., MIMIC-CXR)  
- Extend to multi-step temporal modeling  
- Improve calibration under distribution shift  
- Incorporate clinical metadata  

---

## Author
Banesori Ayekpam
