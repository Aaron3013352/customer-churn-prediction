# Customer Churn Prediction

## Problem
Predict customers at risk of churn to support proactive retention efforts.

## Data
IBM Telco Customer Churn dataset (7,043 customers, mixed numeric and categorical features).

## Approach
- Leakage-safe preprocessing pipeline
- Logistic regression baseline
- Train/validation/test split (70/15/15)
- Threshold selection based on recall and precision constraints
- Final evaluation on a held-out test set

## Results (Test Set)
- ROC-AUC: ~0.86
- PR-AUC: ~0.69
- Churn Recall: ~0.77
- Churn Precision: ~0.54

## Key Takeaways
- The model effectively identifies most churners while controlling outreach volume.
- Threshold tuning is critical for aligning ML outputs with business goals.
- Validation-only decision making prevents overly optimistic performance estimates.
