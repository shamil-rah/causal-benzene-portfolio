# Note on Reproduction

This document provides guidelines for reproducing the results presented in this repository. Due to proprietary restrictions, the full code and raw dataset are not included. However, the methods and pipeline described are sufficient to replicate the **analytical workflow** using similar benzene reaction datasets.

---

## 1. Data Requirements

- Reaction dataset with:
  - Reactant columns (`reactant_000`, `reactant_001`)
  - Product column (`product_000`)
  - Reaction parameters: `rxn_time`, `temperature`, `solvent_000`, `solvent_001`
  - Target yield (`yield_000`)
- Data should be cleaned for invalid SMILES and trailing characters
- Missing reaction conditions should be imputed or filtered

---

## 2. Preprocessing Workflow

1. **Combine Reactants**
   - Concatenate reactant columns into a single canonical SMILES string per reaction.
   - Remove trailing characters or invalid SMILES entries.

2. **Molecular Representation**
   - Generate Morgan fingerprints (radius=2, 1024-bit) for combined SMILES.
   - Fingerprints serve as primary input features.

3. **Feature Processing**
   - Standardize numeric features (temperature, reaction time).
   - One-hot encode categorical features (solvents).

4. **Target Variable**
   - `yield_000` is used as the continuous regression target.

---

## 3. Baseline Model Training

- Use classical ML models (Random Forest, Gradient Boosting) with:
  - Input: Molecular fingerprints + one-hot encoded solvents + standardized numeric features
  - Output: Predicted reaction yield
- Split dataset into training (~90%) and testing (~10%) sets.

---

## 4. Causal Analysis

- For experimental evaluation, implement a counterfactual framework:
  - Simulate intervention on single variables (e.g., temperature, catalyst)
  - Compare predicted yields before and after intervention
  - Identify true causal effect of each reaction parameter

---

## 5. Evaluation Metrics

- **Regression Metrics:** MAE, RMSE
- **Visualization:** 
  - Temperature vs yield
  - Catalyst effect on predicted yield
- Graphs should reflect trends, not precise absolute values (proof-of-concept).

---

## 6. Notes on Reproducibility

- While full datasets and proprietary code are not provided:
  - Methods described are sufficient to implement a similar workflow using public benzene reaction datasets.
  - Pipeline structure:
    1. Data cleaning and preprocessing
    2. Feature engineering (fingerprints, encoded conditions)
    3. Classical ML baseline training
    4. Causal effect estimation
    5. Analysis and visualization
- The workflow is modular and reproducible for any similar reaction datasets.

---

## 7. Disclaimer

This repository is a **proof-of-concept demonstration**. Figures and descriptions summarize internally generated results and are intended to showcase methodology and technical workflow.
