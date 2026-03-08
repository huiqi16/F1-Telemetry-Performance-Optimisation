# F1 Racing Performance Modelling

This repository contains the modelling component of a Formula 1 data science project completed for **DATA3001 at UNSW**.  
The objective of the project is to analyse telemetry data from a racing simulator and identify the driving behaviours that lead to faster corner exit speeds.

---

## Project Overview

Corner exit speed is one of the most important factors influencing lap time in Formula 1.  
This project investigates how driver inputs and vehicle dynamics affect exit speed through **Turns 1–2 of the Albert Park Circuit**.

Using telemetry data from a racing simulator, we built predictive models to identify the key factors contributing to high-performance laps.

---

## Dataset

The modelling uses engineered telemetry features derived from simulator data, including:

- throttle pressure  
- brake pressure  
- steering angle  
- G-forces  
- slip angles  
- distance to apex  
- racing line deviation  

The target variable for prediction is **corner exit speed**.

---

## Models Implemented

Multiple machine learning models were tested and compared:

- Linear Regression
- Elastic Net
- K-Nearest Neighbours Regression (KNN)
- Support Vector Regression (SVR)
- Random Forest
- LightGBM
- XGBoost

Hyperparameter tuning and model comparison were performed to determine the most effective model for predicting exit speed.

---

## Key Insights

The analysis revealed that:

- Early throttle application strongly correlates with higher exit speeds
- Stable steering inputs improve cornering efficiency
- Racing line deviation significantly impacts performance

These findings provide insight into the driving behaviours that maximise performance in the Turn 1–2 sector.

---

## Repository Structure
    model_code/
    ├── Linear_and_ElasticNet_code.ipynb
    ├── KNNR_and_SVR_code.ipynb
    ├── randomforestmodel.ipynb
    ├── LightGBM.ipynb
    ├── XGBoost Minimiser.ipynb

    DATA3001 - F1 Modelling Report (Group 1).pdf


---

## Final Report

The full methodology, model evaluation, and results are documented in:

**DATA3001 - F1 Modelling Report (Group 1).pdf**

---

## Skills Demonstrated

- Feature Engineering
- Regression Modelling
- Machine Learning Model Comparison
- Hyperparameter Tuning
- Python (Pandas, Scikit-learn, LightGBM, XGBoost)
- Data Analysis and Visualisation
