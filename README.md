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
- **Size:** 15 064 rows × 9 columns
- **Features:** Discharge time, voltage, current, charging behavior metrics
- **Target:** RUL — remaining cycles before end of life

---

## Project Structure
```
battery-rul-phm/
├── Battery_RUL.csv        # Dataset
├── notebook.ipynb         # Full PHM pipeline
├── requirements.txt       # Dependencies
└── README.md
```

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

The PHM logic applied here is directly transposable to AEM electrolyzer stacks :

- Battery degradation signals (voltage, discharge time, charging behavior)
  share the same temporal dynamics as stack indicators
  (cell voltage, temperature, pressure)
- The LSTM architecture can be retrained on GEN-HY supervision data
  to predict stack RUL in real time
- EIS/DRT diagnostics could be integrated as additional input features
  to capture AEM-specific degradation mechanisms

---

## Author

**Mohamed Amir Soltani**  
MS Expert Big Data Engineer — UTT  
AI Engineer — Benman Partners  
🔗 [medamirsoltani.github.io](https://medamirsoltani.github.io/)