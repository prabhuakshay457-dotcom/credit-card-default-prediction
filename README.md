# Credit Card Default Prediction

Python analytics project by **Akshay Prabhu and Satya** for Deliverable 1.

## Problem
Use financial attributes and repayment history to predict next-month credit card default and inform voluntary customer support and human review.

## Open in Google Colab
[Open the shared project notebook](https://colab.research.google.com/drive/1822K7WCL6zBHtPDmMaL5btEDFJEgvnGC?usp=sharing)

The notebook downloads the UCI workbook automatically. If that download fails, upload the extracted workbook when prompted in Colab.

## Files
- `Credit_Card_Default_Colab.ipynb`: data checks, exploration, preprocessing, baseline, logistic regression, metrics, and plots.
- `requirements.txt`: versions used for the locally verified results.
- `.gitignore`: excludes downloaded datasets, environments, and temporary files.

## Dataset
Yeh, I. (2009). *Default of Credit Card Clients*. UCI Machine Learning Repository.
https://doi.org/10.24432/C55S3H

Source: https://archive.ics.uci.edu/dataset/350/default+of+credit+card+clients

The dataset contains 30,000 clients, 23 potential predictors, an identifier, and a binary target. The model uses 19 financial and repayment predictors, excluding ID and demographic variables. The data describe Taiwan in 2005; currency values are in New Taiwan dollars. The dataset is licensed CC BY 4.0 and remains hosted by UCI.

## Setup
Recommended local Python version: 3.12.

```bash
python -m pip install -r requirements.txt
```

Open the notebook in Colab or an existing Jupyter environment and run cells in order. Colab supplies the main scientific libraries; the first cell installs xlrd if necessary. Installing these exact versions in Colab is optional and may require restarting the runtime.

## Initial approach
- Stratified 80/20 split: 24,000 training and 6,000 test records; random seed 42.
- Training-only numeric imputation and scaling, plus categorical imputation and one-hot encoding.
- Logistic regression: C=1.0, max_iter=2000, no class weighting, threshold 0.50.
- Majority-class dummy model for comparison.

## Initial test results
| Metric | Logistic regression | Majority baseline |
|---|---:|---:|
| Accuracy | 81.58% | 77.88% |
| Default precision | 65.77% | 0.00% |
| Default recall | 34.89% | 0.00% |
| F1 | 45.59% | 0.00% |
| ROC AUC | 0.7544 | 0.5000 |

Confusion matrix (rows: actual; columns: predicted; order: no default, default):

```text
[[4432, 241],
 [ 864, 463]]
```

These results were verified locally and match the outputs visible in the shared Colab notebook. Saved outputs are retained for review.

## Limitations and next steps
Recall is low: 864 of 1,327 actual defaults were missed. There are 35 repeated records after excluding ID; they were retained because the identifiers differ, but grouped-profile sensitivity analysis is needed. Excluding demographic predictors does not guarantee fairness.

Deliverable 2 will explore training-only cross-validation, regularization, class weighting, threshold selection, calibration, and subgroup errors. Avoid repeated model selection using the inspected test set. This historical educational model is not validated for current lending decisions.

## Planned equal contribution
Akshay: framing, validation, numeric preprocessing, model implementation, and report sections.
Satya: source review, exploratory analysis, categorical preprocessing, evaluation, and report sections.
Each member has 50% of planned effort and reciprocal review responsibilities. This allocation does not assert a completed review history.
