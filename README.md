# AI Aversion Predictive Model

**Author**: Cora Fagan  

## Overview

This project investigates whether individuals who are averse to artificial intelligence (AI) can be identified using survey data from the [2019 Oxford Internet Survey (OxIS)](https://beta.ukdataservice.ac.uk/datacatalogue/studies/study?id=9146).

The target variable is derived from respondents’ agreement with the statement:  
> _"Artificial Intelligence will bring overall positive benefits for society."_

Responses were re-coded into a binary variable:
- `1`: AI-averse (Strongly Disagree or Disagree)
- `0`: Not AI-averse (Neutral to Strongly Agree or Don’t Know)

The goal was to build interpretable classification models to predict AI aversion using demographic, behavioral, and attitudinal data.

---

## Dataset

- **Source**: OxIS 2019 survey (`.dta` format)
- **Target**: `agai` (binary classification)
- **Features**: Over 100 predictors including political views, digital habits, and socio-demographics
- **Preprocessing**:
  - Non-random missing values retained
  - Survey design variables excluded
  - Ordered/categorical variables converted to factors
  - Stratified split: 60% training, 20% validation, 20% test

---

## Methods

### Model Type
- **CART (Classification and Regression Trees)**:
  - Chosen for interpretability and tolerance to mixed-type features
  - No imputation required for missing values

### Class Imbalance Strategies
- Classic upsampling and downsampling
- Class weighting (based on prevalence and manually tuned)
- Bootstrap resampling with cross-validation
- ROC-AUC optimized classification thresholds

### Evaluation Metrics
- **Precision, Recall, F1 Score**
- **ROC Curve and AUC**
- Focused on **minority class performance** (AI-averse group)

---

## Results

- Best model: **Bootstrap ensemble of upsampled CART trees** with AUC-tuned threshold
- Despite tuning:
  - **Low precision/recall on positive class**
  - **Good performance on majority class**
- Final test performance confirmed weak generalizability to out-of-sample AI aversion prediction

---

## Key Findings

- AI aversion is difficult to infer from indirect survey indicators alone
- Models trained on behavior/demographic proxies are insufficient without explicit attitudinal data
- Highlighted the limits of prediction in public opinion modeling, especially with class imbalance

---

## Tech Stack

- **Language**: R
- **Libraries**: `rpart`, `caret`, `pROC`, `tidyverse`, `flextable`, `rpart.plot`, `glmnet`, `haven`
- **Reproducibility**:
  - All code in `.Rmd` file
  - Outputs: ROC curves, sample decision trees, metric tables
  - Final model performance evaluated on held-out test set

---

## File Structure

- ai-aversion-pred-mod.Rmd # Main analysis and model code 
- ai-aversion-pred-mod.html # knitted .html file
- oxis2019ukda.dta # Raw survey data (not included in repo)
- ai-aversion-pred-mod_files # folderes of figures produced in the analysis
- README.md # Project documentation

---

## Limitations

- Limited feature signal for predicting psychological attitudes
- Class imbalance (few AI-averse respondents)
- Dataset from 2019 may not reflect post-2023 AI discourse

---
