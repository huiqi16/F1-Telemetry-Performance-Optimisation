# F1 Telemetry Data Pipeline

This module implements the data pipeline used to process raw racing simulator telemetry data into structured datasets suitable for modelling and analysis.

The pipeline focuses on extracting and engineering features from the **Turn 1–2 sector of the Albert Park Circuit**.

---

## Overview

Raw telemetry data from the simulator is processed through a series of transformation steps to generate two primary datasets:

- **telemetry.csv** – point-level telemetry observations within the analysed track segment
- **summary.csv** – lap-level dataset containing engineered features used for modelling

These datasets provide a clean and structured representation of driver behaviour and vehicle dynamics.

---

## Pipeline Components

The pipeline is implemented in the `pipeline/` directory and consists of several modules:

### cleaning.py
Handles data cleaning tasks including:

- removing invalid telemetry points
- handling missing values
- ensuring consistent telemetry formatting

### loading.py
Loads and prepares the raw telemetry dataset.

### spatial.py
Performs spatial calculations including:

- distance to racing line
- distance to apex
- track position alignment

### telemetry_eng.py
Generates point-level telemetry features such as:

- throttle
- brake
- steering angle
- slip angles
- g-forces

### summary_eng.py
Aggregates telemetry data to create lap-level summary features used for modelling.

### pipeline.py
Coordinates the full pipeline execution.

---

## Generated Outputs

The pipeline generates the following datasets in the `output/` directory:

### telemetry.csv
Point-level telemetry data for each lap within the analysed track segment.

### summary.csv
Lap-level dataset containing engineered features used for modelling and performance analysis.

### racing line reference files

- `left.csv`
- `right.csv`
- `line.csv`

These files describe the reference racing line used for spatial feature calculations.

---

## Running the Pipeline

Run the pipeline using:

```bash
python create_data.py
```
This will generate all processed datasets inside the `output/` directory.

---

## Technologies Used

- Python
- Pandas
- NumPy
- Geometric / spatial calculations


---

# 2️⃣ README for `modelling/`

# F1 Racing Performance Modelling

This repository contains the modelling component of a Formula 1 data science project analysing telemetry data from a racing simulator.

The objective of the project is to identify the driving behaviours and vehicle dynamics that contribute to **higher corner exit speeds**.

---

## Project Overview

Corner exit speed is a key determinant of lap time in Formula 1.  
This project focuses on the **Turn 1–2 sector of the Albert Park Circuit**, analysing how driver inputs and vehicle dynamics affect exit speed.

Using engineered telemetry features, multiple machine learning models were trained to predict and analyse exit speed performance.

---

## Dataset

The modelling uses engineered telemetry features derived from simulator data, including:

- throttle pressure
- brake pressure
- steering angle
- g-forces
- slip angles
- distance to apex
- racing line deviation

The target variable for prediction is **corner exit speed**.

---

## Models Implemented

Several regression models were tested and compared:

- Linear Regression
- Elastic Net
- K-Nearest Neighbours Regression (KNN)
- Support Vector Regression (SVR)
- Random Forest
- LightGBM
- XGBoost

Hyperparameter tuning and model comparison were performed to determine the most effective model.

---

## Key Insights

The analysis suggests that:

- Early throttle application strongly correlates with higher exit speeds
- Stable steering inputs improve cornering efficiency
- Racing line deviation significantly impacts performance

These findings provide insight into driving behaviours that maximise corner exit performance.

---

## Repository Structure
    model_code/
    │
    ├── Linear_and_ElasticNet_code.ipynb
    ├── KNNR_and_SVR_code.ipynb
    ├── randomforestmodel.ipynb
    ├── LightGBM.ipynb
    └── XGBoost Minimiser.ipynb

    DATA3001 - F1 Modelling Report (Group 1).pdf



---

## Final Report

The full methodology, model evaluation, and results are documented in:

**DATA3001 - F1 Modelling Report (Group 1).pdf**

---

## Tech Stack

- Python
- Pandas & NumPy
- Scikit-learn
- LightGBM
- XGBoost
- Jupyter Notebook
- Matplotlib / Seaborn