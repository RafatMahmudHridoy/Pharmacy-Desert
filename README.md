# Machine Learning for Healthcare Accessibility: Developing a Vulnerability Index for U.S. Pharmacy Deserts

This repository archives the dataset and analysis code for the study *"Machine Learning for Healthcare Accessibility: Developing a Vulnerability Index for U.S. Pharmacy Deserts"* (manuscript under review, JMIR).

## Authors

- Nathan Umberger — Purdue University (ORCID: 0009-0004-6601-4699)
- Rafat Mahmud Hridoy — The Pennsylvania State University (ORCID: 0000-0002-4770-9645)
- Azad M. Madni, PhD — University of Southern California (ORCID: 0000-0001-5225-0034)
- Soundar Kumara, PhD — The Pennsylvania State University (ORCID: 0000-0002-7941-8818)

## Contents

| File | Description |
|---|---|
| `Corrected_Pipeline_Pharmacy_Desert.ipynb` | Full analysis notebook (Google Colab / Jupyter). Loads the dataset, performs the leakage-free train/validation/test split, trains and compares five classifiers (Decision Tree, Random Forest, XGBoost, SVM, KNN) plus a logistic-regression baseline via 50-fold repeated cross-validation, evaluates the selected model on the held-out test set, runs a 100-fold robustness check and a leave-one-state-out geographic generalization check, computes SHAP values, and builds the Pharmacy Desert Index (PDI). Includes cells that export every table and figure reported in the manuscript. |
| `county_health_and_pharmacy_desert_dataset_2024.csv` | The organized county-level dataset used in this study (735 U.S. counties across 7 states: Pennsylvania, Ohio, California, Texas, Indiana, Kentucky, and Montana). Predictor variables are drawn from the 2024 County Health Rankings & Roadmaps (CHR) release; the pharmacy-desert outcome variables (`Desert Y/N`, `% Living in Desert`) are drawn from Nguyen et al.'s 2021 GoodRx pharmacy-desert classification (the most recent publicly available classification at the time of analysis). |

## How to reproduce the analysis

1. Open `Corrected_Pipeline_Pharmacy_Desert.ipynb` in Google Colab (or a local Jupyter environment with `xgboost` and `shap` installed).
2. Run the setup/upload cell and, when prompted, upload `county_health_and_pharmacy_desert_dataset_2024.csv`.
3. Run all cells top to bottom, in a single continuous runtime (some later cells depend on models and variables fit earlier in the notebook).
4. The notebook prints every table reported in the manuscript and, in its later cells, saves and downloads the corresponding CSV files (model comparison, cross-validated model comparison, test-set evaluation, 100-fold robustness, PDI results, SHAP weights and direction, per-county predicted probabilities) plus a final "review package" cell that regenerates every figure and a consolidated summary of every reported number in one zip file.

Analysis period: May 2024 – May 2025. Random seed: 42 throughout, for reproducibility.

## License

This repository is released under a Creative Commons Attribution 4.0 International License (CC BY 4.0) — see `LICENSE`. You are free to share and adapt this material for any purpose, provided appropriate credit is given.

## Citation

If you use this dataset or code, please cite the associated paper (citation to be added once published) and this repository (see `CITATION.cff`).

## Contact

For questions about this dataset or code, contact Rafat Mahmud Hridoy (rafathridoy1@iem.kuet.ac.bd).
