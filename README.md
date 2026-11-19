# metalcytotoxdb-ml

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24359516.svg)](https://doi.org/10.5281/zenodo.24359516)


Code for machine learning regression of the cytotoxicity (pIC50) of ruthenium, iridium, rhodium, osmium and rhenium complexes, trained on MetalCytoToxDB (version v2).



Manuscript: *Machine Learning Regression Models for Cytotoxicity Prediction of Transition-Metal Anticancer Complexes: Interpretability and Applicability Domain Analysis*. Aadil I and Jafar Ali Ibrahim S (Vellore Institute of Technology). Submitted to Journal of Cheminformatics.



## Repository layout



```

notebooks/            analysis notebooks (run in numerical order)

figures/              figures produced by the notebooks

results/              performance tables

feature_importance/   feature importance tables

environment.yml       conda environment (Python 3.11.15)

requirements.txt      pip requirements

data/                 not stored here, see "Data" below

models/               not stored here, see "Data" below

```



## Data



1. **Raw dataset.** MetalCytoToxDB, version v2 (published 12 September 2025): https://doi.org/10.5281/zenodo.17106822. Download `MetalCytoToxDB.csv` and place it in `data/`. Please also cite the original publication of the database: https://doi.org/10.1021/acs.jmedchem.5c02755. The dataset licence is stated on its Zenodo record.

2. **Processed data and trained models** (feature matrices, train/test split, and the trained Random Forest, XGBoost, CatBoost and LightGBM models): https://doi.org/10.5281/zenodo.24359516. Unzip the `data` and `models` folders into the root of this repository.



## Installation



```

conda env create -f environment.yml

conda activate cytotoxicity

```



Or, with pip (Python 3.11): `pip install -r requirements.txt`.



## Notebooks



Start Jupyter from inside the `notebooks` folder so that the relative paths work (`cd notebooks`, then `jupyter lab`). Paths are defined in the first cell of each notebook.


| Notebook | Purpose |
|---|---|
| 01_EDA | Exploratory analysis of the dataset |
| 02_Data_cleaning | Cleaning of the raw dataset and calculation of pIC50 |
| 03_RDKit_descriptors | RDKit descriptor calculation |
| 04_Mordred_descriptors | Mordred descriptor calculation (about 7 minutes for 26,801 molecules) |
| 05_Feature_preprocessing_and_split | 80/20 train/test split (random_state=42), then missing-value handling, variance and correlation filtering fitted on the training set only |
| 06_RandomForest | Random Forest: hyperparameter search and evaluation |
| 07_XGBoost | XGBoost: hyperparameter search and evaluation |
| 08_CatBoost | CatBoost: hyperparameter search and evaluation |
| 09_LightGBM | LightGBM: hyperparameter search and evaluation |
| 10a_Explainability_CatBoost | SHAP, permutation importance, PDP/ICE and applicability domain for CatBoost |
| 10b_Explainability_LightGBM | The same analyses for LightGBM |
| 11a_Ablation_CatBoost | Feature-group ablation for CatBoost |
| 11b_Ablation_LightGBM | Feature-group ablation for LightGBM |
| 12_Combined_figures_and_model_check | Bootstrap comparison of CatBoost and LightGBM; assembly of the combined figures |



## Notes on running time and reproducibility



- Notebooks 06 to 09, 11a and 11b contain long hyperparameter searches that can take several hours each. They are provided **with the saved outputs of the original runs**, and the trained models are provided on Zenodo so the test-set results can be checked without retraining.

- Quick check without retraining: after placing `data/` and `models/` in the repository root, run notebook 12.

- All random seeds are fixed in the notebooks.



## Licence



Code: MIT licence (see `LICENSE`).

