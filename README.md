# MBAT-for-seizure-and-SOZ-
a MBAT transformer model with GRU for detection of seizure and SOZ localisation using CHBMIT dataset 

## Overview

This project implements a deep learning pipeline for epileptic seizure detection and seizure onset zone (SOZ) localization using scalp EEG data. The implementation is inspired by the paper:

**MBAT: A Multi-Band Adaptive Transformer Model for Seizure Detection and Seizure Onset Zone Localization from Scalp EEG**.

---

# Project Objective

The goal of this project is to build an interpretable EEG analysis system capable of:

1. Detecting seizure activity from EEG recordings
2. Providing SOZ proxy localization through attention mechanisms
3. Evaluating model generalization across unseen patients

---

# Dataset

## CHB-MIT Scalp EEG Dataset

Dataset Used:

* CHB-MIT EEG Dataset
* Patients used: `chb02` to `chb05`

### Dataset Characteristics

* 19 EEG channels
* Sampling frequency: 256 Hz
* Highly imbalanced dataset

  * Non-seizure segments: 90–98%
  * Seizure segments: 2–10%

---

# Preprocessing Pipeline

The preprocessing stage converts raw EEG recordings into normalized training-ready segments.

## 2. Notch Filtering

A notch filter removes powerline interference.

## 3. Bandpass Filtering

Signals are bandpass filtered to retain useful EEG activity.

## 4. Segmentation

Continuous EEG recordings are divided into fixed-length windows.

Each segment is assigned:

* `0` → Non-seizure
* `1` → Seizure

## 5. Normalization and NPZ Conversion

Processed EEG segments and labels are stored in compressed `.npz` format for efficient loading.

---

# Model Architecture

The model is a code-derived implementation of the MBAT architecture.

Pipeline:

```text
EEG Signal
   ↓
Multi-Band Feature Extraction
   ↓
CNN Band Encoder
   ↓
Transformer Encoder
   ↓
SE Channel Attention
   ↓
GRU Temporal Modelin
   ↓
Detection Head + MIL Attention Pooling
   ↓
Seizure Detection + SOZ Proxy
```

---

## Training Configuration

| Parameter      | Value                 |
| -------------- | --------------------- |
| Epochs         | 20                    |
| Batch Size     | 32                    |
| Optimizer      | AdamW                 |
| Loss Function  | BCEWithLogitsLoss     |
| Early Stopping | Enabled               |
| Evaluation     | LOPO Cross Validation |

---

# Model Performance

## MBAT + GRU Results

| Metric      | Score  |
| ----------- | ------ |
| Sensitivity | 71.91% |
| Specificity | 80.71% |
| AUC-ROC     | 82.23% |

---

# Technologies Used

## Libraries

* Python
* PyTorch
* NumPy
* Pandas
* Matplotlib
* SciPy
* MNE
* Scikit-learn

---

# Reference

## Research Paper

Chuntao Zhang et al.

"MBAT: A Multi-Band Adaptive Transformer Model for Seizure Detection and Seizure Onset Zone Localization from Scalp EEG"

2024.

---

# Source Files

* Presentation slides
* MBAT implementation notebook: `MBAT_FINAL_FINAL(3).ipynb`
