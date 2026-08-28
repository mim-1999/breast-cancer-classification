# Breast Cancer Classification (Logistic Regression)

A self-directed logistic regression project predicting whether a breast tumor is malignant or benign, using the Breast Cancer Wisconsin (Diagnostic) dataset. 

## Project Overview
This project uses cell nuclei measurements from digitized breast tissue images to predict a binary diagnosis (malignant vs. benign). Beyond fitting a model, the focus was on rigorous feature analysis: diagnosing severe multicollinearity across geometrically related features, distinguishing genuine outliers from informative extreme values, and reasoning about classification thresholds in a medical context.

## Key Steps

**EDA**
- Verified class balance (62.7% benign / 37.3% malignant) and established a majority-class baseline
- Compared feature distributions (radius, concavity, area) across malignant/benign groups via histograms
- Identified that extreme values ("outliers" by standard IQR rules) in size- and shape-related features were overwhelmingly malignant cases — i.e., signal, not noise — and should not be removed

**Multicollinearity Diagnosis**
- Initial VIF check revealed extreme multicollinearity (VIF > 3900) among geometrically related features (radius, perimeter, area — all derived from the same underlying measurement)
- Iteratively dropped redundant features within each measurement group (mean/SE/worst), reducing max VIF from ~3950 to ~38 across two rounds of analysis, guided by geometric reasoning rather than blind trial-and-error

**Modeling**
- Logistic Regression on the reduced, scaled feature set
- Evaluated via confusion matrix, precision/recall/F1 (per class), and ROC-AUC

**Threshold Analysis**
- Given the medical context (a missed malignant case is more costly than a false alarm), tested raising the classification threshold to reduce false negatives for malignancy
- Found the model's one missed malignant case had a predicted P(benign) of 0.90 — confidently wrong — illustrating that threshold tuning has limits when a model is highly confident in an incorrect prediction

## Results
- **Accuracy:** 98%
- **ROC-AUC:** 0.995
- **Recall (malignant):** 98% (41/42 correctly identified)
- **Baseline comparison:** far exceeds the 62.7% majority-class baseline

## Key Insight
Cell size (radius, in all three measured forms) and shape irregularity (concavity, texture) were the dominant predictors of malignancy, consistent with clinical intuition that cancerous cells tend to be larger and more irregularly shaped than healthy cells. This matched patterns already visible during EDA, giving consistent evidence across the exploratory and modeling stages.

## Tech Stack
Python, pandas, scikit-learn, statsmodels, matplotlib
