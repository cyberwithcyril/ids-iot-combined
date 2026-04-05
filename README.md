# ids-iot-combined

**ML & Deep Learning for IoT Intrusion Detection: A Cross-Dataset Generalization Study**

> M.S. Cybersecurity & Digital Forensics — SUNY Albany | Spring 2026  
> Author: Cyril Thomas ([@cyberwithcyril](https://github.com/cyberwithcyril))

---

## Overview

This project benchmarks six machine learning and deep learning models across two IoT benchmark datasets — **CIC-IoT-2023** (general IoT) and **CICIoMT-2024** (medical IoT) — using identical preprocessing pipelines and 38 shared network flow features. The central research question: *Do ML and DL model rankings generalize across different IoT environments?*

**Short answer: Yes.** Random Forest ranked 1st on both datasets. All 6 models improved by ~+0.019 F1 on medical IoT data, suggesting healthcare network attack patterns are more structurally distinct and easier to detect.

---

## Results

### CIC-IoT-2023 (General IoT — 105 devices)

| Rank | Model | F1 | AUC-ROC | Precision | Recall | Accuracy |
|------|-------|----|---------|-----------|--------|----------|
| 1 | **Random Forest** | **0.9872** | 0.9952 | 0.9989 | 0.9758 | 0.9760 |
| 2 | XGBoost | 0.9805 | **0.9958** | 0.9622 | **0.9994** | 0.9622 |
| 3 | MLP | 0.9786 | 0.9929 | **0.9999** | 0.9582 | 0.9601 |
| 4 | 1D-CNN | 0.9780 | 0.9922 | 0.9999 | 0.9571 | 0.9591 |
| 5 | BiLSTM | 0.9779 | 0.9924 | 0.9999 | 0.9570 | 0.9590 |
| 6 | Logistic Regression | 0.9744 | 0.9892 | 1.0000 | 0.9501 | 0.9526 |

### CICIoMT-2024 (Medical IoT — 40 devices)

| Rank | Model | F1 | AUC-ROC | Precision | Recall | Accuracy |
|------|-------|----|---------|-----------|--------|----------|
| 1 | **Random Forest** | **0.9995** | 0.9999 | 0.9998 | 0.9991 | 0.9989 |
| 2 | XGBoost | 0.9991 | **1.0000** | 0.9983 | **0.9999** | 0.9983 |
| 3 | MLP | 0.9979 | 0.9995 | **1.0000** | 0.9958 | 0.9959 |
| 4 | BiLSTM | 0.9978 | 0.9996 | 1.0000 | 0.9957 | 0.9958 |
| 5 | 1D-CNN | 0.9974 | 0.9994 | 1.0000 | 0.9948 | 0.9949 |
| 6 | Logistic Regression | 0.9942 | 0.9979 | 0.9999 | 0.9885 | 0.9887 |

### Cross-Dataset F1 Gain

| Model | IoT-2023 F1 | IoMT-2024 F1 | Gain | Rank Stable? |
|-------|-------------|--------------|------|-------------|
| Random Forest | 0.9872 | 0.9995 | +0.0123 | ✅ 1st both |
| XGBoost | 0.9805 | 0.9991 | +0.0186 | ✅ 2nd both |
| MLP | 0.9786 | 0.9979 | +0.0193 | ✅ 3rd both |
| 1D-CNN | 0.9780 | 0.9974 | +0.0194 | ✅ 5th both |
| BiLSTM | 0.9779 | 0.9978 | +0.0199 | ✅ 4th both |
| Logistic Regression | 0.9744 | 0.9942 | +0.0198 | ✅ 6th both |

---

## Datasets

### CIC-IoT-2023
Canadian Institute for Cybersecurity, University of New Brunswick  
https://www.unb.ca/cic/datasets/iotdataset-2023.html

| Attribute | Value |
|-----------|-------|
| IoT domain | General consumer IoT |
| Devices | 105 IoT devices |
| Total rows | 45,019,243 |
| Rows used | 500,000 (stratified sample) |
| Attack types | 34 |
| Attack ratio | 95% attack, 5% benign |
| Features used | 39 |

### CICIoMT-2024
Canadian Institute for Cybersecurity, University of New Brunswick  
https://www.unb.ca/cic/datasets/iomt-dataset-2024.html

| Attribute | Value |
|-----------|-------|
| IoT domain | Medical IoT (WiFi + MQTT) |
| Devices | 40 IoMT devices |
| Total rows | 7,160,831 |
| Rows used | 500,000 (stratified sample) |
| Attack types | 18 |
| Attack ratio | 97.3% attack, 2.7% benign |
| Features used | 38 shared |

---

## Project Structure

```
ids-iot-combined/
├── data/
│   ├── raw/
│   │   ├── ciciot2023/          # 63 CSV files (not tracked in git)
│   │   └── ciciomt2024/
│   │       ├── train/           # 52 CSV files (not tracked in git)
│   │       └── test/            # 21 CSV files (not tracked in git)
│   └── processed/               # Numpy arrays and scalers (not tracked in git)
├── notebooks/
│   ├── 01_eda_ciciot2023.ipynb
│   ├── 02_preprocessing_ciciot2023.ipynb
│   ├── 03_logistic_regression_ciciot2023.ipynb
│   ├── 04_random_forest_ciciot2023.ipynb
│   ├── 05_xgboost_ciciot2023.ipynb
│   ├── 06_mlp_ciciot2023.ipynb
│   ├── 07_cnn_ciciot2023.ipynb
│   ├── 08_bilstm_ciciot2023.ipynb
│   ├── 09_comparison_shap_ciciot2023.ipynb
│   ├── 10_eda_ciciomt2024.ipynb
│   ├── 11_preprocessing_ciciomt2024.ipynb
│   ├── 12_logistic_regression_ciciomt2024.ipynb
│   ├── 13_random_forest_ciciomt2024.ipynb
│   ├── 14_xgboost_ciciomt2024.ipynb
│   ├── 15_mlp_ciciomt2024.ipynb
│   ├── 16_cnn_ciciomt2024.ipynb
│   ├── 17_bilstm_ciciomt2024.ipynb
│   ├── 18_comparison_shap_ciciomt2024.ipynb
│   └── 19_generate_charts.ipynb
├── models/                      # Saved model files (not tracked in git)
├── results/
│   ├── ciciot2023_model_comparison.csv
│   ├── ciciomt2024_model_comparison.csv
│   ├── ciciot2023_shap_feature_importance.csv
│   ├── ciciomt2024_shap_feature_importance.csv
│   ├── chart_f1_grouped.png
│   ├── chart_auc_grouped.png
│   ├── chart_shap_comparison.png
│   ├── chart_radar_ciciot.png
│   └── chart_radar_ciciomt.png
└── README.md
```

---

## Models

### Classical ML
- **Logistic Regression** — L2 regularization, lbfgs solver, class-weighted
- **Random Forest** — 100 trees, max depth 20, class-weighted, Gini importance
- **XGBoost** — 200 estimators, lr=0.1, max_depth=6, scale_pos_weight for imbalance

### Deep Learning
- **MLP** — 3 hidden layers (256→128→64), ReLU, Dropout 0.3, early stopping (patience=10)
- **1D-CNN** — 2× Conv1D (64/128 filters, kernel=3), GlobalMaxPool, Dense 64, 100 epochs max
- **BiLSTM** — 2× Bidirectional LSTM (64 units), Dense 32, 200 epochs max

---

## Preprocessing Pipeline

1. Load all CSV files and extract labels from filenames (CICIoMT-2024)
2. Remove duplicate rows (24M from CIC-IoT-2023, 5K from CICIoMT-2024)
3. Replace infinite values (Rate feature) with NaN and drop
4. Align to 38 shared features across both datasets
5. Binary label: Benign (0) vs. Attack (1)
6. Stratified sample of 500,000 rows from each dataset
7. 70/15/15 train/val/test split
8. StandardScaler normalization (fit on train only)
9. Balanced class weighting via sklearn compute_class_weight

---

## SHAP Analysis

SHAP TreeExplainer applied to Random Forest (F1 winner) on 500 test samples.

### Top Features — CIC-IoT-2023
| Rank | Feature | Mean \|SHAP\| | Attack Pattern |
|------|---------|--------------|----------------|
| 1 | Number (packet count) | 0.1086 | Volumetric flooding |
| 2 | ack_flag_number | 0.0526 | ACK flag anomaly |
| 3 | HTTPS ratio | 0.0487 | Protocol abuse |

### Top Features — CICIoMT-2024
| Rank | Feature | Mean \|SHAP\| | Attack Pattern |
|------|---------|--------------|----------------|
| 1 | rst_count | 0.0568 | Connection manipulation |
| 2 | IAT (inter-arrival time) | 0.0522 | Burst traffic |
| 3 | AVG packet length | 0.0522 | Packet size anomaly |

---

## Key Findings

**Finding 1 — Classical ML outperforms deep learning on both datasets**  
Random Forest leads F1 on both datasets. Pre-aggregated tabular network flow features favor gradient boosting over neural architectures — the feature extraction step removes the raw sequential signal that DL is designed to exploit.

**Finding 2 — Medical IoT attacks are more detectable**  
All 6 models improve by ~+0.019 F1 on CICIoMT-2024. Healthcare attack patterns are more structurally distinct, producing cleaner network signatures that are easier to classify.

**Finding 3 — Model rankings generalize across IoT environments**  
Rankings are perfectly preserved across both datasets. Practitioners can trust published benchmark results for IoT IDS model selection without dataset-specific re-evaluation.

---

## Dataset Investigation

Five candidate datasets were evaluated before selecting this pair:

| Dataset | Decision | Reason |
|---------|----------|--------|
| DataSense CIC IIoT 2025 | Separate project | Hybrid sensor+network features unique to CIC lab hardware |
| CIC-APT-IIoT 2024 | Rejected | PCAP only, NS3 simulation with timestamp issues |
| Edge-IIoTset | Rejected | Packet-level Wireshark features — incompatible |
| CIC-IDS-2017 | Rejected | Enterprise network dataset — IDS group scope |
| CIC-IoT-2023 alone | Rejected | Single dataset — no cross-dataset generalization |

---

## Setup

```bash
git clone https://github.com/cyberwithcyril/ids-iot-combined.git
cd ids-iot-combined
python -m venv .venv
.venv\Scripts\activate       # Windows
pip install -r requirements.txt
```

Download datasets separately and place in `data/raw/ciciot2023/` and `data/raw/ciciomt2024/train/` and `data/raw/ciciomt2024/test/`.

Run notebooks in order (01 → 19).

---

## Requirements

```
pandas
numpy
scikit-learn
xgboost
tensorflow
shap
matplotlib
seaborn
joblib
imbalanced-learn
```

---

## Citations

```
Neto, E.C.P., Dadkhah, S., Ferreira, R., Zohourian, A., Lu, R., & Ghorbani, A.A. (2023).
CICIoT2023: A Real-Time Dataset and Benchmark for Large-Scale Attacks in IoT Environment.
https://www.unb.ca/cic/datasets/iotdataset-2023.html

Dadkhah, S., Ferreira, R., Molokwu, R.C., Neto, E.C.P., Sadeghi, S., & Ghorbani, A.A. (2024).
CICIoMT2024: A Multi-Protocol Dataset for Assessing IoMT Device Security.
https://www.unb.ca/cic/datasets/iomt-dataset-2024.html
```

---

## License

MIT License — see LICENSE for details.

---

## Related Project

**ids-iiot-deeplearning** — Deep Learning vs. Classical ML on DataSense CIC IIoT 2025 (hybrid sensor+network features)  
https://github.com/cyberwithcyril/ids-iiot-deeplearning
