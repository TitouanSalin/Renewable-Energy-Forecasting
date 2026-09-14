# Variable Renewable Energy Forecasting

**Machine Learning for Climate & Energy · École Polytechnique · Sep-Dec 2025**

Machine learning pipeline for predicting **monthly solar photovoltaic and onshore wind capacity factors across French regions** from climate variables derived from **NASA MERRA-2 reanalysis data**.

The project investigates how climate information can be transformed into regional renewable-energy production estimates, from raw climate-data preprocessing and feature engineering to model selection, hyperparameter optimization, and performance analysis.

---

## Overview

The increasing penetration of variable renewable energy makes understanding the relationship between climate conditions and electricity production increasingly important.

This project develops supervised machine learning models to estimate monthly capacity factors for:

- **Solar photovoltaic power**
- **Onshore wind power**

across different French regions.

The models combine observed regional capacity factors with climate variables extracted from MERRA-2, allowing us to study both predictive performance and the relationship between meteorological conditions and renewable-energy production.

---

## Machine Learning Pipeline

```text
        MERRA-2 Climate Data
                 │
                 ▼
      ┌─────────────────────┐
      │ Spatial Aggregation │
      │  by French Region   │
      └──────────┬──────────┘
                 │
                 ▼
      ┌─────────────────────┐
      │ Monthly Aggregation │
      │ + Feature Engineering│
      └──────────┬──────────┘
                 │
                 ▼
      ┌─────────────────────┐
      │ Feature Analysis &  │
      │     Selection       │
      └──────────┬──────────┘
                 │
          ┌──────┴──────┐
          ▼             ▼
    Solar Dataset    Wind Dataset
          │             │
          ▼             ▼
      ┌─────────────────────┐
      │  Model Benchmarking │
      │ & Hyperparameter    │
      │    Optimization     │
      └──────────┬──────────┘
                 │
                 ▼
        Capacity-Factor
           Prediction
```

---

## Data

### Renewable-Energy Data

The target variables are **monthly regional capacity factors** for solar photovoltaic and onshore wind generation.

Capacity factor represents actual electricity generation relative to the maximum generation that would be obtained if the installed capacity operated continuously at full power.

### Climate Data

Climate predictors are derived from **MERRA-2 reanalysis data** and include variables related to:

- Surface radiation
- Temperature
- Air density
- Specific humidity
- Zonal wind
- Meridional wind

Daily climate observations are spatially aggregated over French regions and then aggregated at monthly resolution to match the renewable-energy observations.

Additional statistics such as quantiles and variance are used to capture **intra-month climate variability** beyond simple monthly averages.

---

## Modeling Approach

The project compares several supervised machine learning approaches for mapping regional climate conditions to renewable-energy capacity factors.

The workflow includes:

1. **Climate-data preprocessing**  
   Aggregation of gridded MERRA-2 variables by region and month.

2. **Feature engineering**  
   Construction of climate predictors describing both average conditions and intra-month variability.

3. **Feature analysis and selection**  
   Investigation of the relationships between meteorological variables and solar/wind production.

4. **Model benchmarking**  
   Comparison of regularized linear models and tree-based ensemble methods.

5. **Hyperparameter optimization**  
   Model parameters are tuned to improve generalization performance.

6. **Evaluation**  
   Predictions are assessed using metrics including **R², MAE, and RMSE**.

---

## Selected Results

### Solar Photovoltaic

The solar models achieved strong predictive performance, with the best experiments reaching approximately:

**R² = 0.94**

This highlights the strong relationship between regional solar capacity factors and climate variables such as surface radiation.

The analysis also revealed that evaluation methodology matters: temporal changes in the relationship between climate variables and observed capacity factors can create **distribution shift**, making chronological prediction more difficult than randomized train/test evaluation.

### Onshore Wind

Wind capacity factors proved more difficult to predict from monthly aggregated climate information.

The optimized wind model achieved approximately:

**Test R² = 0.66**

with:

- **MAE ≈ 0.037**
- **RMSE ≈ 0.049**

The gap between training and testing performance also highlights the greater difficulty of generalizing wind-power relationships from the available regional and temporally aggregated predictors.

---

## Key Takeaways

The project illustrates several challenges involved in applying machine learning to renewable-energy forecasting:

- Climate reanalysis data can provide strong predictive signals for regional renewable-energy production.
- Solar capacity factors are particularly well captured by climate-derived predictors.
- Wind prediction is more challenging at monthly and regional resolution.
- Feature engineering can capture information that is lost through simple temporal averaging.
- Random train/test splits can overestimate performance when the underlying data-generating process evolves over time.
- Temporal distribution shift is therefore an important consideration when evaluating climate-driven energy models.

---

## Tech Stack

**Python · scikit-learn · Pandas · NumPy · xarray · Matplotlib · Jupyter**

The project combines climate-data processing, feature engineering, supervised machine learning, hyperparameter optimization, model evaluation, and scientific visualization.

---

## Repository Structure

```text
Renewable-Energy-Forecasting/
│
├── data/                         # Climate and renewable-energy datasets
│
├── VRE_forcasting.ipynb      # Complete analysis and ML pipeline
│
├── VRE_forcasting_report.html
│                                 # Project presentation
│
└── README.md                     # Project overview and documentation
```

---

## Running the Analysis

The complete workflow is implemented in the Jupyter notebook:

**`VRE_forcasting.ipynb`**

It contains the data preprocessing, exploratory analysis, feature engineering, model training, hyperparameter optimization, evaluation, and visualizations used in the project.

The HTML report provides a condensed walkthrough of the methodology and main results.

---

## Authors

This project was developed collaboratively by:

- **Titouan Salin**
- **Alice Vergnes**

as part of coursework at **École Polytechnique**.
