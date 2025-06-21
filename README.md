# Electrocoagulation-Project

# Electrocoagulation Prediction

A regression-based project to predict electric current and residence time in an electrocoagulation treatment process, using experimental parameters such as contaminant concentration, pH, electrode properties, and reactor settings.

---

## 📋 Project Overview

Electrocoagulation is a water-treatment technique that uses electrical current to remove dissolved contaminants (e.g., arsenic, fluoride). This project demonstrates an end-to-end pipeline to:

1. **Load & clean** experimental data  
2. **Explore** feature distributions and correlations  
3. **Train & compare** multiple regression models  
4. **Evaluate** predictive performance on held-out data  
5. **Draw conclusions** and recommend best models  

---

## 🗄 Dataset

- **Source file:** `Project_updated_trial.csv`  
- **Rows:** 371  
- **Columns (after renaming):**  
  - Contaminant (As, F)  
  - Initial & Final Concentration (mg/L)  
  - % Removal  
  - Initial pH  
  - Current (A)  
  - Electrode Gap (cm)  
  - Current Density (A/m²)  
  - Residence Time (min)  
  - Reactor Volume (mL)  
  - Electrode Material (Al, Fe, Fe-Al)  
  - Electrode Area (m²)  

---

## 🔄 Data Preprocessing

- **Dropped** irrelevant IDs (S.No, Reference No.) and non-informative “Batch/Continuous” (98% Batch).  
- **Imputed** missing values:  
  - pH → 7 (median)  
  - Gap → 1 cm (median)  
- **Standardized** categorical labels for electrode materials.  
- **Scaled** numerical features (StandardScaler) and **one-hot encoded** electrode material.

---

## 🔍 Exploratory Analysis

- **Descriptive statistics** highlighted skewed concentration distributions and bimodal pH.  
- **Correlation heatmap** revealed:  
  - Strong negative correlation between % removal and final concentration  
  - High positive correlation between current and current density  
  - Moderate links (e.g., gap vs final concentration)  

---

## 🤖 Modeling & Evaluation

### Models Compared
- **Linear Regression**, **Ridge**, **Lasso**  
- **Support Vector Regression** (linear kernel)  
- **Decision Tree Regressor**  
- **Random Forest Regressor** (500 trees)  
- **XGBoost Regressor** (500 trees)

### Targets & Splits
- Predict **Current** and **Residence Time** separately  
- Train/test split: 80/20 (random_state=42)

### Performance (R² on test set)

| Model            | As_Current | As_Time | F_Current | F_Time |
|------------------|-----------:|--------:|----------:|-------:|
| Linear           | 0.73       | 0.54    | 0.82      | 0.80   |
| Ridge            | 0.74       | 0.50    | 0.82      | 0.80   |
| Lasso            | 0.84       | 0.53    | 0.80      | 0.80   |
| SVR (linear)     | 0.74       | 0.61    | 0.82      | 0.40   |
| **Decision Tree**| **0.96**   | 0.36    | **0.98**  | 0.71   |
| **Random Forest**| **0.96**   | **0.77**| **0.98**  | **0.91**|
| XGBoost          | **0.97**   | 0.65    | 0.85      | 0.80   |

> Best overall: **Random Forest** for both current and time (highest average R²)  
> XGBoost excels at arsenic current; Decision Tree is surprisingly strong on fluoride current.

---

## ⚠️ Potential Limitations

- **Residence Time** is harder to predict (lower R²), suggesting missing features or complex dynamics.  
- **Data imbalance:** Batch mode dominates—model may not generalize to continuous operation.  
- **Correlation-based multicollinearity:** Current & density highly correlated; future work could remove redundant features.  
- **Limited dataset size** (371 points) and two contaminants only—further experiments may improve robustness.

---

## 🚀 Future Work

- **Feature engineering:** Transform skewed variables (e.g., log-transform concentrations), derive interaction terms.  
- **Data collection:** Gather more experiments across a wider range of operating modes and contaminants.  
- **Advanced models:** Try deep learning or Gaussian process regression for uncertainty quantification.  
- **Deployment:** Build a simple web API or dashboard to input process parameters and get real-time predictions.

---

## 📂 Repository Structure

```text
├── data/
│   └── Project_updated_trial.csv
├── notebooks/
│   └── Electrocoagulation_prediction.ipynb
├── src/
│   ├── preprocessing.py
│   ├── modeling.py
│   └── evaluation.py
├── README.md
└── requirements.txt
