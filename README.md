# covid19-hospital-and-icu-length-of-stay

Repository for the paper submitted at IEEE ICHI (IEEE International Conference on Healthcare Informatics) 2023 conference


# Title
Predicting ICU and Hospital Length of Stay for COVID-19 Patients

# Abstract
The accurate prediction of a patient’s length of stay is a crucial aspect for healthcare providers, as it enables effective resource management and preparation for patient care. This includes the development of appropriate medical plans, estimation of expenses for insurance companies, and budget planning for patient relatives. In the context of the ongoing global COVID-19 pandemic, predicting the length of stay has become increasingly important. Our study focused on predicting the duration of stay in the intensive care unit (ICU) and total hospital stay using synthetic COVID-19 data from the SyntheticMass library. Machine learning algorithms, including LightGBM gradient boosting and two Transformer models (Linear and Periodic), were utilized for this prediction. Through experimental analysis, we found that the gradient boosting algorithm performed best, particularly after undergoing parameter optimization. The mean absolute error (MAE) of predicting ICU stay is less than one day, and the overall hospital stay MAE is 1.5 days.

# Notebook Description

- hospital_merged_num_cat_top20lbmfi.ipynb
	- This notebook is for hospital length of stay model prediction. during data pre-processing and preparation; 166 features were selected from 11 files (patients, careplans, conditions, encounters, medications, observations, allergies, devices, imaging studies, immunizations and providers). 166 features includes 123 numerical features and 23 categorical features. Out of 166 features, top 20 features were selected based on lightgbm feature importance for model building. 
- hospital_merged_num_cat_top30lbmfi_v1.ipynb (**referred in ieee paper**)
	- Top 30 out of 166 (numerical and categorical) features were used based on lightgbm feature importance in this hospital LOS notebook.
- hospital_merged_num_cat_top30lbmfi_v2.ipynb
	- Top 30 out of 166 (numerical and categorical) features were used based on lightgbm feature importance in this hospital LOS notebook and compared to above notebook, some additional graphs have been included such as validation/training loss.
- hospital_merged_num_cat_top40lbmfi.ipynb
	- Top 40 out of 166 (numerical and categorical) features were used based on lightgbm feature importance in this hospital LOS notebook.
- icu_merged_num_cat_top20lbmfi.ipynb
	- This notebook is for icu length of stay model prediction. during data pre-processing and preparation; 148 features were selected from 11 files (patients, careplans, conditions, encounters, medications, observations, allergies, devices, imaging studies, immunizations and providers). 148 files includes 106 numerical features and 42 categorical features. Out of 148 features, total 20 features were selected based on lightgbm feature importance for model building. 
- icu_merged_num_cat_top30lbmfi_v1.ipynb (**referred in ieee paper**)
	- Top 30 out of 148 (numerical and categorical) features were used based on lightgbm feature importance in this icu LOS notebook.
- icu_merged_num_cat_top30lbmfi_v2.ipynb
	- Top 30 out of 148 (numerical and categorical) features were used based on lightgbm feature importance in this icu LOS notebook and compared to above icu top 30 notebook, some additional graphs have been included such as validation/training loss. 
- icu_merged_num_cat_top40lbmfi.ipynb
	- Top 40 out of 148 (numerical and categorical) features were used based on lightgbm feature importance in this icu LOS notebook.
- icu_merged_num_cat_top50lbmfi.ipynb
	- Top 50 out of 148 (numerical and categorical) features were used based on lightgbm feature importance in this icu LOS notebook.
- old_code/hospital_v3_merged_num_cat.ipynb
	- Total 166 features used in this study. lightgbm feature importance was applied.
- old_code/hospital_v5_merged_num_cat_selected.ipynb
	- Only selected 45 out of 166 features most relevant to covid including 28 numerical and 17 categorical were used for this hospital LOS notebook.
- old_code/icu_v3_merged_num_cat.ipynb
	- Total 148 features used in this icu length of stay notebook. lightgbm feature importance was applied.
- old_code/icu_v4_merged_num_cat_top20_20.ipynb
	- In this ICU length of stay notebook, top 20 out of 106 numerical and top 20 out of 42 categorical features so total 40 features were used based on transformer model feature importance. 
- old_code/icu_v4_merged_num_cat_top40.ipynb
	- In this ICU length of stay notebook, top 40 out of 148 features were used based on transformer model feature importance. 
- old_code/icu_v5_merged_num_cat_selected.ipynb
	- Only selected 47 out of 148 features most relevant to covid including 27 numerical and 20 categorical were used in this icu LOS notebook.


# Dataset

Dataset in this project has been used from Synthetic Mass Library which can be downloaded from [here](https://synthea.mitre.org/downloads). this dataset contains total 16 files including patients, careplans, conditions, encounters, medications, observations, allergies, devices, imaging studies, immunizations, organizations, payer transitions, payers, procedures, providers, and supplies. there are two types of datasets available: 

- Covid-19 100k: consists 124,150 patients information; used in this project as training set (during data preperation and later split of 80/20 during model training)
- Covid-19 10k: consists 12,352 patients information; used as test set

# Pre-requisites

- Programming Language: Python (3.8.* or later)
- Required python libs to install: 
		- scikit-learn
		- tensorflow
		- [tabtransformertf](https://github.com/aruberts/TabTransformerTF)
		- [optuna](https://optuna.org/)
		- Numpy, pandas, matplotlib
	
# Notes

- Each file (notebook# 1-9) runs lightgbm and 2 transformer (FT Piecewise Linear and Periodic Encoding) models all together.
- Lightgbm model runs in this order:
	-  Without using parameter optimization
	-  RandomizedSearchCV with optimized parameters.
- FT Transformer model runs in this order:
	- Piecewise Linear Encoding without Parameter optimization
	- Piecewise Periodic Encoding without optimized parameters
	- Piecewise Periodic Encoding with Parameter optimization
	- Piecewise Periodic Encoding with Tuned parameters (tuned parameters passed from 3)
	- Piecewise Linear Encoding with Parameter optimization
	- Piecewise Linear Encoding with Tuned parameters (tuned parameters passed from 5)

