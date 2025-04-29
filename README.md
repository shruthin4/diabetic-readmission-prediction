
# Predicting 30-Day Readmission Risk in Diabetic Patients Using Machine Learning

![Python](https://img.shields.io/badge/Language-Python-blue.svg)
![Model](https://img.shields.io/badge/Model-LightGBM-success)


This project aims to predict **30-day hospital readmissions** for diabetic patients using health records  from the UCI Diabetes dataset. Through advanced data preprocessing, domain-informed feature engineering, class imbalance handling, and machine learning, I  developed a robust model with strong recall and explainability.

## Project Structure

```
Readmission-Prediction-Project/
├── README.md
├── Documentation.pdf                # Full project documentation  
├── data/
│   ├── diabetic_data.csv
│   └── IDS_mapping.csv
│   └── cleaned_data.csv
├── Code.ipynb                     # End-to-end notebook with code & markdowns
├── requirements.txt               # Requirements
└── lightgbm_tuned_model.joblib    # Saved model
├── images/                        # SHAP and feature importance plots
└── LICENSE
```

## Objective

To build an interpretable machine learning model that identifies diabetic patients at risk of hospital readmission within 30 days of discharge.

## Dataset Overview

- **Source**: UCI Diabetes 130-US hospitals dataset
- **Records**: ~100,000 hospital encounters
- **Features**: Demographics, diagnoses, procedures, medications, and more
- **Target Variable**: `readmitted` (<30 days vs. not)

## Workflow Summary

1. **Data Cleaning & Preparation**
   - Handled missing values, removed irrelevant features
   - Standardized categorical codes and merged mappings
2. **Feature Engineering**
   - Domain-aware features: insulin use, age-hospitalization interaction, discharge flags
   - Created risk indicators and binary medication features
3. **EDA & Insights**
   - Explored trends in readmissions, diagnosis categories, and medication patterns
4. **Model Development**
   - Algorithms: Logistic Regression, Random Forest, LightGBM, XGBoost
   - Used pipelines, cross-validation, and hyperparameter tuning
   - Applied SMOTE & class weights to handle imbalance
5. **Evaluation**
   - Precision, recall, F1-score, confusion matrix
   - Feature importance & SHAP plots for explainability

## Best Model Summary

| Model                  | Recall | Precision | F1-Score | Accuracy |
|------------------------|--------|-----------|----------|----------|
| LightGBM (Tuned)       | 0.62   | 0.18      | 0.28     | 0.65     |
| XGBoost (Tuned)        | 0.60   | 0.18      | 0.27     | 0.65     |
| Logistic Regression    | 0.54   | 0.17      | 0.25     | 0.66     |
| SMOTE + LightGBM (0.1) | 0.81   | 0.16      | 0.24     | 0.52     |

## Key Risk Factors Identified

- **number_inpatient** – strongest indicator of future readmission
- **discharged_to_facility**, **discharged_home** – key discharge destinations
- **insulin_used**, **diabetesMedication** – treatment signals
- **age_inpatient_interaction** – combined demographic + utilization risk
- **num_lab_procedures**, **num_medications** – signal patient complexity

## Real-World Considerations

Although our tuned LightGBM model achieved a **recall of 0.62** and **F1-score of 0.28**, it's important to understand that structured EHR data alone has limitations in predicting real-world outcomes.

Several important factors influencing readmission risk are **not captured in this dataset**, such as:

- Mental health status or behavioral factors
- Medication adherence post-discharge
- Availability of caregiver support at home
- Environmental or socioeconomic stressors
- Sudden medical complications or accidents

These limitations explain why precision remained moderate (~18%) despite strong recall. In healthcare, **missing a high-risk patient** can be more costly than flagging a false positive — which is why recall was prioritized in this project.

This model is therefore best used as a **clinical decision support tool** — helping care teams identify and prioritize at-risk patients, while still relying on human expertise for final decisions.



## Installation

```bash
pip install -r requirements.txt
```

## Reproducibility

- Python 3.9+
- Trained and evaluated using Jupyter Notebook
- All preprocessing handled via `Pipeline()`

## Author

**Shruthin Reddy**  
Master's Student – University of Louisville  
Email: [shruthinreddysainapuram@gmail.com]  


