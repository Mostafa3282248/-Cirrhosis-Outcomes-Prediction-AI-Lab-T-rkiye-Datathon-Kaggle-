
# Cirrhosis Outcomes Prediction – AI Lab Türkiye Datathon (Kaggle)

## 1. Project Overview

This project tackles a medical machine learning problem from the **AI Lab Türkiye Datathon: Cirrhosis Outcomes Multi-Class Prediction** (Kaggle).

Given clinical data for cirrhosis patients, the goal is to predict the probability of three possible outcomes at a fixed follow-up time `N_Days`:

- **C**  – Censored (alive)
- **CL** – Alive due to liver transplant
- **D**  – Deceased

The competition uses **multi-class log-loss** as the evaluation metric.  
This repository contains a complete end-to-end solution:

- Data loading and exploratory analysis  
- Feature engineering  
- Multiple baseline and advanced models  
- Out-of-fold (OOF) evaluation with stratified cross-validation  
- Blended ensemble of tree-based models  
- Error analysis and clinical interpretation  

---

## 2. Data

The dataset is AI-generated but mimics real cirrhosis patient data. Files:

- `train.csv` – training data with target `Status`
- `test.csv` – test data without labels
- `sample_submission.csv` – example submission format

Basic characteristics:

- **Train size**: 15,000 rows
- **Features**: ~43 columns (demographics, labs, clinical indicators)
- **Target**: `Status` ∈ {C, CL, D}

Class distribution in `train`:

- C  : 10,188 (≈ 67.9%)
- D  : 4,457  (≈ 29.7%)
- CL :   355  (≈  2.4%)

This makes **CL** a rare and challenging class.

Key feature types:

- Demographics: `Age`, `Sex`
- Disease stage / follow-up: `N_Days`, `Stage`
- Laboratory values: `Bilirubin`, `Albumin`, `Prothrombin`, `Cholesterol`, `SGOT`, `Alk_Phos`, `Platelets`, etc.
- Categorical clinical indicators: `Ascites`, `Hepatomegaly`, `Spiders`, `Edema`, `Drug`, etc.

---

## 3. Evaluation Metric

The competition uses **multi-class logarithmic loss**:

\[
\text{LogLoss} = - \frac{1}{N} \sum_{i=1}^{N} \sum_{k=1}^{3} y_{i,k}\log(p_{i,k})
\]

Where:

- \(N\) = number of samples in the test set  
- \(k \in \{C, CL, D\}\)  
- \(y_{i,k} = 1\) if sample \(i\) belongs to class \(k\), otherwise 0  
- \(p_{i,k}\) = predicted probability that sample \(i\) belongs to class \(k\)

Submissions must include:

```text
id,Status_C,Status_CL,Status_D
