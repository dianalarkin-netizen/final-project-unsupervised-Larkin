# Feature Discovery for Fraud Detection in Insurance Claims

**Google Colab Notebook:** https://colab.research.google.com/drive/13Fysqi84bF4ypixaplgd3QGawKjA0Bj0?usp=sharing

**Video Presentation:** https://1drv.ms/v/c/faf6cbb1d6e30397/IQBiuGP_am6yRqTVExaOjRsoAS-QxoMfx4e7u7-rQnD8jgA?e=fXqgZO

## Overview
This project explores how **unsupervised learning** can uncover hidden patterns in insurance claims data and improve fraud detection. By applying clustering and PCA, we discovered meaningful claim segments and integrated them into predictive models to test whether these features enhanced accuracy.

---

## Dataset
- **Source:** Insurance claims dataset (1,000 rows, 40 variables)
- **Variables:** Included demographics, policy details, incident characteristics, and fraud labels
- **Target Variable:** `fraud_reported` (Yes/No)
- **Key Data Notes:**
  - Class imbalance: ~75% legitimate claims vs. ~25% fraudulent claims
  - Data cleaning addressed missing values and ambiguous categories
  - Random seeds set for reproducibility

---

## Methods

### Feature Discovery
- **Clustering:** Applied K‑Means, tested multiple k values, selected k=2 using elbow and silhouette methods
- **Segments Identified:**
  - **Straightforward Minor Claims:** Single‑vehicle, minor damage, clearer property damage categories, ~23% fraud rate
  - **Severe Multi‑Vehicle Losses:** Multi‑vehicle collisions, severe damage or total loss, ambiguous property damage, ~27% fraud rate
- **PCA:** Reduced dimensionality for visualization; explained ~17% of variance but confirmed cluster separation

### Predictive Modeling
- **Models Tested:**
  - Logistic Regression (baseline)
  - Random Forest
  - Gradient Boosting
- **Evaluation Metrics:** Accuracy, Precision, Recall, F1 Score
- **Comparison:** Models tested with and without discovered features (cluster membership, PCA components)

---

## Findings

### Model Performance Comparison
| Model                          | Accuracy | Precision | Recall | F1 Score |
|--------------------------------|----------|-----------|--------|----------|
| Logistic Regression (Baseline) | 0.8500   | 0.6508    | 0.8367 | 0.7321   |
| Logistic Regression (Features) | 0.8500   | 0.6508    | 0.8367 | 0.7321   |
| Random Forest (Baseline)       | 0.8100   | 0.6410    | 0.5102 | 0.5682   |
| Random Forest (Features)       | 0.8150   | 0.6579    | 0.5102 | 0.5747   |
| Gradient Boosting (Baseline)   | 0.8050   | 0.6136    | 0.5510 | 0.5806   |
| Gradient Boosting (Features)   | 0.8100   | 0.6170    | 0.5918 | 0.6042   |

- **Logistic Regression** remained the strongest overall model.
- **Gradient Boosting** showed modest improvement in recall and F1 when cluster features were added.
- **Random Forest** gained slightly in precision but remained weaker in recall.

---

## Business Recommendations
1. **Segment claims handling** by cluster (minor vs. severe).
2. **Use Logistic Regression** as the baseline operational model.
3. **Enhance Gradient Boosting** with resampling/tuning to improve recall.
4. **Monitor ambiguous property damage categories** closely, as they align with higher fraud risk.
5. **Expand feature engineering** to capture more complex fraud patterns.

---

## Limitations & Next Steps
- PCA explained limited variance; primarily useful for visualization.
- Fraud imbalance remains a challenge; future work should test advanced resampling methods (e.g., SMOTE).
- External validation is needed to confirm generalizability.
- With more time, deeper feature engineering and ensemble tuning could yield stronger improvements.

---

## Key Insight
Fraud risk is **not random** — it clusters around incident complexity and policy structures.  Unsupervised learning adds valuable context, even if predictive gains are modest, and sets the foundation for stronger fraud detection models in the future.
