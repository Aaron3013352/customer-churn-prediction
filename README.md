# Customer Churn Prediction — Industry-Style ML Pipeline

## Overview
This project predicts customer churn using the IBM Telco Customer Churn dataset.  
It was developed in two stages: an initial raw-data baseline and a refactored,
industry-style machine learning pipeline that emphasizes reproducibility,
leakage prevention, and business-aligned evaluation.

The final solution mirrors how churn models are built and evaluated in real
production environments.

---

## Project Evolution

### Phase 1 — Raw Baseline Modeling
The project originally began as a single-notebook workflow that:
- Loaded raw Excel/CSV data directly
- Performed cleaning and leakage handling in pandas
- Trained and evaluated a baseline churn model

This version is preserved for comparison in:

**`04_modeling_raw_baseline.ipynb`**

It demonstrates common early-stage modeling practices and highlights the
limitations of mixing data preparation and modeling logic.

---

### Phase 2 — Industry-Style Pipeline (Final)
The project was then refactored into a modular, production-oriented workflow:

SQL Extraction → EDA → Modeling → Business Decisioning

Key improvements:
- SQL-based feature extraction
- Clear separation of concerns across notebooks
- Leakage-safe preprocessing pipelines
- Validation-based threshold selection
- One-time final test set evaluation

This refactored pipeline is the primary version of the project.

---

## Repository Structure
customer-churn-prediction/
│
├── notebooks/
│ ├── 01_sql_extract.ipynb
│ ├── 02_eda.ipynb
│ ├── 03_modeling_sql_features.ipynb
│ └── 04_modeling_raw_baseline.ipynb
│
├── data/
│ ├── raw/
│ └── processed/
│
├── reports/
│ ├── figures/
│ │ ├── pr_curve_validation.png
│ │ └── test_set_results.png
│ └── metrics.json
│
├── requirements.txt
└── README.md


---

## Notebook Guide

### 01 — SQL Feature Extraction
**`01_sql_extract.ipynb`**

- Loads raw Telco churn data
- Simulates a production database using SQLite
- Performs SQL-based aggregation and feature selection
- Outputs a clean, model-ready dataset

**Purpose:** Demonstrates SQL usage and production-style data preparation.

---

### 02 — Exploratory Data Analysis
**`02_eda.ipynb`**

- Explores the processed feature dataset
- Analyzes churn distribution and key drivers
- Provides business intuition for downstream modeling

**Purpose:** Data understanding and insight generation (no modeling).

---

### 03 — Final Modeling (SQL Features)
**`03_modeling_sql_features.ipynb`** ⭐ **Primary Notebook**

- Loads SQL-extracted Parquet features
- Builds a leakage-safe preprocessing + modeling pipeline
- Uses stratified train/validation/test splits
- Evaluates with ROC-AUC and PR-AUC
- Selects a decision threshold based on business trade-offs
- Performs a one-time final test set evaluation

**Purpose:** Represents the final, industry-ready churn model.

---

### 04 — Raw Baseline Modeling
**`04_modeling_raw_baseline.ipynb`**

- Models churn directly from raw data
- Handles cleaning and leakage in pandas
- Serves as a comparison against the SQL-based pipeline

**Purpose:** Illustrates why a structured, SQL-driven pipeline is preferable for
reproducibility and governance.

---

## Final Results (SQL-Based Model)

Final test set performance at a business-aligned threshold:

- **ROC-AUC:** ~0.86  
- **PR-AUC:** ~0.69  
- **Recall (Churn):** ~0.97  
- **Precision (Churn):** ~0.40  

This operating point prioritizes identifying at-risk customers, reflecting a
retention-focused strategy where missing a churner is more costly than
contacting a non-churner.

---

## Key Takeaways

- SQL-based feature extraction improves reproducibility and auditability
- Separating EDA, modeling, and data prep reduces leakage risk
- Threshold selection is as important as model choice for business impact
- One-time test set evaluation provides a realistic estimate of performance

---

## Technologies Used

- Python (pandas, NumPy, scikit-learn)
- SQL (SQLite)
- Jupyter / Google Colab
- Git & GitHub
- matplotlib / seaborn

---

## Future Work

- Cost-based optimization of decision thresholds
- Uplift modeling for targeted retention campaigns
- Monitoring data drift and retraining strategies
- Comparison with tree-based models

