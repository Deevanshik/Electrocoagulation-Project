# Electrocoagulation Prediction

This project focuses on predicting two key outputs of the electrocoagulation water treatment process — **electric current** and **residence time** — using various experimental parameters.

---

## 📌 Project Objective

To build machine learning models that can accurately predict the operating current and treatment duration based on input features such as contaminant concentration, pH, electrode configuration, and reactor setup.

---

## 🧪 Dataset

- Contains **371 experimental records**
- Features include:
  - Contaminant type (As, F)
  - Initial/Final concentrations
  - % removal, pH, electrode gap, current density
  - Electrode material, reactor volume, and more

---

## ⚙️ Workflow Summary

1. **Data Cleaning & Preprocessing**
   - Renamed and cleaned columns
   - Imputed missing values
   - Standardized categories and scaled features

2. **Exploratory Data Analysis**
   - Summary statistics
   - Distribution plots
   - Correlation heatmaps

3. **Modeling**
   - Trained multiple regressors: Linear, SVR, Decision Tree, Random Forest, XGBoost
   - Evaluated using R² on test set
   - Separate models for arsenic and fluoride datasets

---

## ✅ Key Outcomes

- **Random Forest** and **XGBoost** showed the best performance for both current and time prediction.
- Achieved **R² scores above 0.96** for current prediction and up to **0.91** for residence time.

---

## ⚠️ Observations

- Residence time is harder to model than current.
- Slight data imbalance (mostly batch mode operations).
- Feature correlations and data size may limit generalization.

---

## 📁 Files

- `Electrocoagulation_prediction.ipynb`: Main notebook with all details
- `Project_updated_trial.csv`: Dataset used

---

## 📌 Note

For detailed analysis, model comparison, and code, refer to the Jupyter notebook in the repository.
