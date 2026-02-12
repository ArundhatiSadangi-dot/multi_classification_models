# Multiclass Wine Quality Classification (White Wine — UCI)

This project implements and deploys six classification models on the **UCI Wine Quality (White)** dataset. It follows the assignment requirements: modeling, evaluation, Streamlit UI, and deployment.

## Problem Statement
Predict **wine quality** (integer score 0–10) for **white wines** using **12 physicochemical features**. This is framed as a **multiclass classification** problem. (Dataset source: UCI Wine Quality)  
**UCI dataset page:** https://archive.ics.uci.edu/ml/datasets/Wine+Quality  
**Direct CSV (white wine):** https://archive.ics.uci.edu/ml/machine-learning-databases/wine-quality/winequality-white.csv

> The UCI page confirms the white wine subset has **4,898 instances**, **11 input features** plus **1 target (quality)**, and provides the CSV files for both red and white wines. Classes are **ordered** and **imbalanced**.  
> Citation: UCI Machine Learning Repository — Wine Quality. (Accessed Feb 2026)

## Dataset Description ✅
- **Source:** UCI Machine Learning Repository — Wine Quality (White)  
- **Download (CSV):** `winequality-white.csv` (semicolon `;` separated)  
- **Instances:** 4,898  
- **Features:** 12 (11 inputs: fixed_acidity, volatile_acidity, citric_acid, residual_sugar, chlorides, free_sulfur_dioxide, total_sulfur_dioxide, density, pH, sulphates, alcohol; **target**: quality [0–10])  
- **Task:** Multiclass classification (quality levels)  
- **Note:** We treat the problem as **multiclass classification** (not regression). Class distribution is skewed; macro-averaged metrics are reported.

## Models Used & Metrics (to be filled after training)
We trained the following models on the same data split:

1. Logistic Regression  
2. Decision Tree Classifier  
3. K-Nearest Neighbors (KNN)  
4. Gaussian Naive Bayes  
5. Random Forest (Ensemble)  
6. XGBoost (Ensemble)

**Reported metrics on the test split:** Accuracy, **AUC (macro OVR)**, Precision (macro), Recall (macro), F1 (macro), **MCC**.

After you run `python train_models.py`, copy values from `models/metrics_summary.csv` into the table below:

| ML Model Name | Accuracy | AUC (macro) | Precision (macro) | Recall (macro) | F1 (macro) | MCC |
|---|---:|---:|---:|---:|---:|---:|
| Logistic Regression | | | | | | |
| Decision Tree | | | | | | |
| kNN | | | | | | |
| Naive Bayes | | | | | | |
| Random Forest (Ensemble) | | | | | | |
| XGBoost (Ensemble) | | | | | | |

## Observations (add after training)
Typical observations for this dataset:

- **Logistic Regression** – Benefits from scaling; can underfit non-linearities but gives stable macro metrics.  
- **Decision Tree** – Captures non-linear boundaries; may overfit without constraints.  
- **kNN** – Sensitive to scaling and `k`; mid-range neighbors often perform well.  
- **Naive Bayes** – Very fast; independence assumption can hurt with correlated features (e.g., SO2 measures).  
- **Random Forest** – Strong tabular baseline; robust and often among top F1.  
- **XGBoost** – Typically best or close; tune learning rate, depth, estimators for gains.

## How to Run (BITS Virtual Lab)

```bash
# 1) Install dependencies
pip install -r requirements.txt

# 2) (Optional) Cache the CSV locally
mkdir -p data
wget -O data/winequality-white.csv https://archive.ics.uci.edu/ml/machine-learning-databases/wine-quality/winequality-white.csv

# 3) Train all models, compute metrics, export artifacts
python train_models.py

# Artifacts saved to ./models
# - *.joblib (six models)
# - metrics_summary.csv (table for README)
# - figs/*_cm.png (confusion matrices)
# - test_holdout.csv (ready to upload to the app)

# 4) Run Streamlit app
streamlit run app.py
```

## Streamlit App Features (required by assignment)
- ✅ CSV upload (test data only)  
- ✅ Model selection dropdown  
- ✅ Display of evaluation metrics  
- ✅ Confusion matrix + classification report  

## Deployment (Streamlit Community Cloud)
1. Push this repo to **GitHub** (public).  
2. Go to **https://streamlit.io/cloud** → **New app**.  
3. Select your repo, branch `main`, file `app.py`, click **Deploy**.  
4. Ensure `requirements.txt` includes `xgboost`.  
5. If the deployed app cannot find model files, run training locally and **commit the generated `models/*.joblib`**.

## Repo Structure
```
project-folder/
│-- app.py
│-- train_models.py
│-- requirements.txt
│-- README.md
│-- models/
│   ├─ *.joblib
│   ├─ metrics_summary.csv
│   ├─ test_holdout.csv
│   └─ figs/*_cm.png
└-- data/
    └─ winequality-white.csv  # optional cache
```

## References
- **UCI Machine Learning Repository — Wine Quality** (dataset description, CSV files, features and target):  
  https://archive.ics.uci.edu/ml/datasets/Wine+Quality  
  Direct CSV (white): https://archive.ics.uci.edu/ml/machine-learning-databases/wine-quality/winequality-white.csv
```
(Cortez, P., Cerdeira, A., Almeida, F., Matos, T., & Reis, J. (2009). Modeling wine preferences by data mining from physicochemical properties. *Decision Support Systems*.)
```
