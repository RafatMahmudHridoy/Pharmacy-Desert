# Pharmacy Desert Index (PDI) for U.S. Counties: Data and Code

Data and analysis code for:

> Umberger N, Hridoy RM, Madni AM, Kumara S. *Machine Learning for Healthcare Accessibility: Developing a Pharmacy Desert Index for U.S. Counties.* Manuscript under review, JMIR Formative Research (manuscript #100048).

Nathan Umberger and Rafat Mahmud Hridoy contributed equally to this work.

## What the study does

Using county-level demographic, socioeconomic, and healthcare data for 734 counties in seven states (Pennsylvania, Ohio, California, Texas, Indiana, Kentucky, and Montana), the study:

1. trains and compares five machine learning classifiers (Decision Tree, Random Forest, XGBoost, Support Vector Machine, K-Nearest Neighbors) plus a logistic-regression baseline to classify each county's current pharmacy-desert status;
2. uses SHAP values from the selected model (XGBoost) to identify the features most associated with pharmacy-desert status; and
3. builds the Pharmacy Desert Index (PDI), a descriptive composite score that combines the SHAP-based weights of the 11 most important features with each county's percentile ranks on those features.

The PDI describes where a county stands, relative to the other counties in the sample, on the characteristics most associated with pharmacy-desert status. It does not measure vulnerability, probability, or future risk, and the associations it summarizes are not causal.

## Files

| File | Description |
|---|---|
| `2021_All_county_combined_full_dataset_corrected.csv` | County dataset: 735 rows (counties), 57 columns. Predictors from the 2021 County Health Rankings & Roadmaps release; pharmacy-desert share from Nguyen et al. (GoodRx, September 2021). |
| `Corrected_Pipeline_Pharmacy_Desert_2021_OUTCOME50.ipynb` | Full analysis notebook, with the saved outputs of the run reported in the paper. |
| `CITATION.cff` | Citation metadata. |
| `LICENSE` | License. |

### Key dataset columns

- `County, State`: county identifier.
- `% Living in Desert`: share of the county's population living in pharmacy-desert census tracts (Nguyen et al.). A census tract is a pharmacy desert when the average driving time to its three nearest pharmacies exceeds 15 minutes.
- `Desert Y/N`: county outcome, `Y` when more than 50% of the population lives in pharmacy-desert tracts (Nguyen et al.'s county definition), otherwise `N`. 289 counties are `Y` and 445 are `N`. San Francisco, California has no pharmacy-desert data and is left blank; it is excluded from the analysis.
- Provider ratios (`Primary Care Physicians Ratio`, `Dentist Ratio`, `Mental Health Provider Ratio`, `Other Primary Care Provider Ratio`) are stored as text such as `1904:1` and converted to providers per person in the notebook.
- The remaining columns are County Health Rankings measures. Ten of them (Homicide Rate, PTSD, Psychosis, % Disconnected Youth, Depression, Child Mortality Rate, Infant Mortality Rate, Drug Overdose Mortality Rate, Suicide rate, HIV Prevalence Rate) have more than 20% missing values and are removed in the notebook, leaving 44 candidate features.

## How to reproduce the results

1. Open `Corrected_Pipeline_Pharmacy_Desert_2021_OUTCOME50.ipynb` in Google Colab (or Jupyter with Python 3, pandas, scikit-learn, xgboost, shap, scipy, seaborn).
2. Run all cells from top to bottom and upload `2021_All_county_combined_full_dataset_corrected.csv` when prompted.
3. The notebook prints every number reported in the paper and saves the result tables as CSV files and a review package (zip). The first cell of the notebook explains which section produces each table and figure.

Random seeds are fixed (`RANDOM_STATE = 42`). Results can differ slightly with other library versions.

### Main results (from the saved run)

- 289 of 734 counties (39.4%) are pharmacy deserts.
- Model selection (50-fold repeated cross-validation): XGBoost balanced accuracy 0.842 ± 0.030, AUC 0.923 ± 0.021.
- Held-out test set (148 counties): AUC 0.959, balanced accuracy 0.896.
- Most important features: % Rural, Population, Traffic Volume.
- PDI tiers: 242 low, 236 medium, 256 high (above 0.6) counties.

## Data sources

- County Health Rankings & Roadmaps. 2021 County Health Rankings release. University of Wisconsin Population Health Institute. https://www.countyhealthrankings.org/health-data
- Nguyen A, van Meijgaard J, Kim S, Marsh T. Mapping healthcare deserts. GoodRx; September 2021.

## Version history

- **v3.0.0**: analysis for the second revision. Predictors from the 2021 County Health Rankings release (temporally aligned with the 2021 outcome); outcome coded with Nguyen et al.'s county definition (more than 50% of the population in pharmacy-desert tracts); class-imbalance correction applied once per model; per-fold and test-set exports for every model.
- **v1.0.0 and v2.0.0**: earlier versions, archived on Zenodo, with predictors from the 2024 release and an outcome that marked any county with residents in a pharmacy-desert tract as a desert. They are superseded by v3.0.0.

## License

Released under the Creative Commons Attribution 4.0 International License (CC BY 4.0). See `LICENSE`.
