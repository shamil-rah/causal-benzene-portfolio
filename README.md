Causal Benzene Reaction Predictor

This repository implements a proof-of-concept system that combines classical machine learning and modern causal inference to predict and analyze the yield of benzene-related chemical reactions. The project aims to bridge the gap between predictive modeling and causal reasoning in computational chemistry, providing actionable insights for synthetic chemists while maintaining reproducibility and clarity.

1. Project Overview

Accurately predicting chemical reaction yields is a critical challenge in computational and synthetic chemistry. Traditional machine learning methods offer predictive power but are limited to correlational insights. This project addresses that limitation by introducing causal inference techniques that can estimate the effect of experimental conditions on reaction yield.

The system operates in two stages:

Baseline Machine Learning Regression
Predicts reaction yield using molecular descriptors and encoded experimental conditions.

Causal Inference Analysis
Estimates the true causal effects of variables such as solvent, temperature, and catalyst through do-calculus, intervention simulations, and graphical causal models.

2. Key Objectives

Predict yields of benzene-related reactions with classical machine learning models.

Quantify the influence of experimental parameters using causal inference.

Provide a reproducible, lightweight, and modular pipeline that can run on a standard laptop.

Enable “what-if” intervention analysis (e.g., estimating the impact of changing temperature or solvent).

Lay the foundation for scalable, explainable AI applications in chemistry.

3. Core Technologies
Component	Technology
Language	Python
ML Framework	scikit-learn
Molecular Descriptors	rdkit
Data Handling	pandas, numpy
Visualization	matplotlib, seaborn
Causal Inference	dowhy (with optional support for causalml)
Environment	Runs locally on standard hardware, no GPU required
4. Repository Structure
causal-benzene-predictor/
│
├── data/
│   └── benzene_reactions.csv              # Input dataset
│
├── src/
│   ├── data_prep.py                       # Preprocessing and feature engineering
│   ├── ml_model.py                        # Baseline ML training and evaluation
│   └── causal_analysis.py                 # Causal inference and intervention experiments
│
├── main.ipynb                             # Orchestrates full workflow (training + causal)
├── NOTE_ON_REPRODUCTION.md                # Reproduction and environment setup guide
├── PROJECT_REPORT.md                      # Technical background and methodology
└── README.md                              # Project documentation

5. Dataset

Source: Publicly available chemical reaction datasets, including benzene transformations, can be obtained from:

Open Reaction Database (ORD): https://www.open-reaction-database.org

USPTO Reaction Dataset: https://figshare.com/articles/dataset/USPTO-Data/11712803

Required fields:

reactant_smiles — SMILES string representation of the reactant.

solvent — solvent used in the reaction.

catalyst — catalyst employed.

temperature — reaction temperature (°C).

time — reaction time (hours or minutes, depending on dataset).

yield — measured yield of the reaction (percentage).

Filtering Criteria:
Only benzene reactions are included, identified by the SMILES substructure c1ccccc1.

6. Feature Engineering and Preprocessing

Molecular fingerprints are generated using Morgan circular fingerprints (radius 2, 1024 bits).

Categorical variables (solvent, catalyst) are encoded using LabelEncoder.

Continuous variables (temperature, time) are normalized with StandardScaler.

Final feature matrix: concatenation of fingerprints, encoded categorical variables, and normalized continuous variables.

7. Machine Learning Baseline

Models Implemented:

Random Forest Regressor

Gradient Boosting Regressor

Evaluation Metrics:

Mean Absolute Error (MAE)

Root Mean Square Error (RMSE)

Workflow:

Split the data into train and test sets (80/20).

Train the models with default hyperparameters.

Evaluate predictive performance using MAE and RMSE.

Visualize predicted vs. actual yields with scatter plots.

8. Causal Inference Extension

Framework: dowhy

Causal Graph Example:

catalyst -> temperature -> yield
catalyst -> yield
solvent -> yield


Methods Used:

Graphical causal model construction

Backdoor adjustment with linear regression estimator

Intervention simulations (e.g., do(temperature = x))

Refutation tests (placebo treatments, data subsets)

Output:

Causal effect estimates

Counterfactual yield predictions under hypothetical interventions

Model summary and refutation results

9. Reproducibility

The pipeline is designed to run on standard laptops without specialized hardware.
It requires only Python ≥3.8 and standard open-source packages.

Quick Start:

git clone https://github.com/yourusername/causal-benzene-predictor.git
cd causal-benzene-predictor
pip install -r requirements.txt


Running the Workflow:

jupyter notebook main.ipynb


Or directly via Python scripts:

python src/data_prep.py
python src/ml_model.py
python src/causal_analysis.py

10. Expected Outputs

Preprocessed dataset with molecular descriptors and encoded variables.

MAE and RMSE scores for baseline ML models.

Scatter plots of predicted vs. actual yields.

Causal effect estimate for key variables (temperature, solvent, catalyst).

Intervention results demonstrating hypothetical outcome shifts.

Reproducible, documented codebase ready for extension.

11. Limitations and Future Work

The current proof-of-concept uses a limited benzene dataset. Scaling to broader reaction classes will require additional data curation and graph expansion.

Causal models are based on domain-informed assumptions and may not capture unknown confounders.

Hyperparameter optimization is minimal and can be expanded.

Integration with larger reaction knowledge graphs is planned for future iterations.

12. Citation

If you use or build upon this project, please cite or reference the repository appropriately.

@software{causal_benzene_predictor,
  author = {Project Contributors},
  title = {Causal Benzene Reaction Predictor: Integrating ML and Causal Inference for Reaction Yield Prediction},
  year = {2025},
  url = {https://github.com/yourusername/causal-benzene-predictor}
}

13. License

This project is released under the MIT License.
You are free to use, modify, and distribute the code with attribution.

14. Contact

For inquiries, contributions, or issues, please open an issue on the repository or contact the maintainers via GitHub.
