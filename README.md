# F1 Chicane Performance Optimisation

> **Can machine learning on simulator data prescribe optimal driver inputs?**  
> Using 1,032 laps of racing telemetry to identify the trigger points that minimise chicane time at Albert Park Turns 1–2.

---

## Overview

In Formula 1, tenths of a second through a single corner complex can decide a race outcome. This project applies machine learning to simulator telemetry to identify the **optimal combination of braking, steering, and throttle trigger points** through the technically demanding Turns 1–2 chicane at the Albert Park Circuit.

The project ran in two phases, each handled by a different group:

| Phase | What happened | My contribution |
|---|---|---|
| **Data Engineering** | Raw frame-level telemetry → clean lap-level dataset | Pipeline design, spatial feature engineering, lap aggregation |
| **Modelling** | ML model comparison + differential evolution optimisation | EDA, data cleaning, all modelling, optimisation |

---

## Headline Results

| Model | RMSE (ms) | Adj. R² | MAE (ms) |
|---|---|---|---|
| Linear Regression | 1,707.5 | 0.325 | 982.5 |
| Elastic Net | 1,409.6 | 0.540 | 879.4 |
| KNN Regressor | 468.6 | 0.037 | 312.1 |
| Random Forest | 341.3 | 0.818 | 192.6 |
| LightGBM | 265.9 | 0.679 | 166.6 |
| XGBoost | 189.7 | 0.856 | 127.3 |
| **SVR (selected) ✓** | **98.6** | **0.924** | **75.7** |

SVR with a linear kernel (C=1000, ε=100) outperformed every other model by a wide margin. The linear kernel result is notable — it suggests the relationship between correctly-engineered trigger-point features and lap time is approximately linear once noisy and mislabelled features are resolved.

> **Key insight:** Targeted IQR outlier removal improved SVR's adjusted R² from –1.36 to **0.924**. Data quality work delivered more lift than any amount of hyperparameter tuning.

---

## Optimisation

With SVR validated, SciPy's `differential_evolution` was used to find the global minimum — the input combination that minimises predicted chicane time.

**Optimal trigger point profile:**

| Trigger | Speed | Time | Action |
|---|---|---|---|
| BPS / THE | 319 km/h | 2,897–3,118 ms | Begin braking; lift off throttle |
| STS | 274 km/h | 3,760 ms | Initiate steering into Turn 1 |
| BPE / THS | 152–172 km/h | 3,714–4,429 ms | Release brake; begin throttle re-application |
| STM | 175 km/h | 5,616 ms | Steering midpoint through Turn 2 |
| STE | 241 km/h | 8,284 ms | Steering neutral; full acceleration |

**Target chicane time: 11,266.63 ms (~11.27 seconds)**  
Verified against real laps using KNN — the recommendation is physically achievable.

---

## Key Findings

1. **Exit phase dominates.** Steer End (STE) features are the strongest predictors of lap time. How a driver exits the corner matters more than how they enter it.
2. **Early throttle is critical.** Throttle re-application at ~152 km/h directly correlates with higher exit speed into the Turn 3 straight.
3. **Tight braking window.** Optimal braking sits within a 2m window at 249–275m lap distance — a concrete, actionable coaching reference.

---

## Dataset

- **1,032 simulator laps** · **255 raw features** · reduced to **57 driver-controlled features** for modelling
- Frame-level telemetry collapsed to one row per lap via 7 key trigger point snapshots
- Features include: speed, throttle, brake, steering angle, lap time, lap distance, world X/Y position at each trigger

---

## Repository Structure

```
F1-Racing-Simulator/
│
├── data-product/          # Phase 1 — raw telemetry → structured dataset
│   ├── pipeline/
│   │   ├── cleaning.py
│   │   ├── loading.py
│   │   ├── spatial.py
│   │   ├── telemetry_eng.py
│   │   ├── summary_eng.py
│   │   └── pipeline.py
│   ├── create_data.py
│   └── README.md
│
├── modelling/              # Phase 2 — ML modelling + optimisation
│   ├── Linear_and_ElasticNet_code.ipynb
│   ├── KNNR_and_SVR_code.ipynb
│   ├── randomforestmodel.ipynb
│   ├── LightGBM.ipynb
│   ├── XGBoost_Minimiser.ipynb
│   ├── fixed_final_data_product.csv
│   └── README.md
│
├── requirements.txt
└── README.md               ← you are here
```

---

## Tech Stack

![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat-square&logo=python)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-grey?style=flat-square&logo=scikit-learn)
![XGBoost](https://img.shields.io/badge/XGBoost-grey?style=flat-square)
![LightGBM](https://img.shields.io/badge/LightGBM-grey?style=flat-square)
![SciPy](https://img.shields.io/badge/SciPy-grey?style=flat-square&logo=scipy)

`Python` · `Pandas` · `NumPy` · `Scikit-learn` · `XGBoost` · `LightGBM` · `SciPy` · `Shapely` · `Matplotlib` · `Seaborn`

---

## Context

Academic project — DATA3001, UNSW. The project was structured so that different student groups handled data engineering and modelling separately. The modelling group (which I was part of) used a dataset produced by a separate data engineering group, then conducted all EDA, cleaning, modelling, and optimisation independently.
