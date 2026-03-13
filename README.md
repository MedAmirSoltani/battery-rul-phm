# Battery RUL Prediction — PHM Pipeline with LSTM

**Author:** Mohamed Amir Soltani  
**Date:** March 2026

---

## Overview

This project implements a complete **Prognostics and Health Management (PHM)** 
pipeline to predict the **Remaining Useful Life (RUL)** of batteries using 
electrochemical degradation data.

The approach is directly transposable to **AEM electrolyzer stacks** — 
replacing battery features with stack indicators (cell voltage, temperature, 
pressure, EIS/DRT diagnostics) to enable real-time prognostics in industrial 
supervision systems.

---

## Pipeline
```
Raw Data → Cleaning (IQR) → EDA → Feature Scaling → LSTM Model → RUL Prediction
```

| Step | Description |
|------|-------------|
| **Loading** | 15 064 cycles × 9 electrochemical variables |
| **Cleaning** | IQR-based outlier removal — 451 anomalies removed (~3%) |
| **EDA** | Distributions, correlations, degradation curve analysis |
| **Modeling** | 2-layer LSTM with Dropout, sliding window of 30 cycles |
| **Evaluation** | R² = 0.90 — MAE = 77 cycles |

---

## Results

| Metric | Value |
|--------|-------|
| R² | 0.9029 |
| MAE | 77.50 cycles |
| RMSE | 95.93 cycles |

The model captures **90% of RUL variance** trained in only 7 epochs.

---

## Dataset

- **Source:** [Kaggle — Battery Remaining Useful Life (RUL)](https://www.kaggle.com/datasets/ignaciovinuales/battery-remaining-useful-life-rul)
- **Features:** Discharge time, voltage, current, charging behavior metrics
- **Target:** RUL — remaining cycles before end of life

---

## Installation
```bash
git clone https://github.com/medamirsoltani/battery-rul-phm.git
cd battery-rul-phm
pip install -r requirements.txt
jupyter notebook notebook.ipynb
```

---

## Requirements
```
pandas
numpy
matplotlib
seaborn
scikit-learn
tensorflow
jupyter
```

---

## Link to AEM Electrolyzers

This pipeline mirrors the PHM objectives for AEM stacks:

- **Health Indicators** → cell voltage decay, temperature gradients, pressure
- **Degradation modeling** → same LSTM architecture, retrained on stack data
- **Online prognostics** → deployable in industrial supervision systems
- **EIS/DRT integration** → additional diagnostic features for AEM-specific degradation

---

## Author

**Mohamed Amir Soltani**  
MS Expert Big Data Engineer — UTT  
AI Engineer — Benman Partners  
🔗 [medamirsoltani.github.io](https://medamirsoltani.github.io/)