# Time Series Analysis and Energy Demand Forecasting

[**English**](README.md) | [Deutsch](README.de.md)

## Project Overview

This project explores two time-series tasks:

1. **Personal step-count analysis:** Exploratory analysis of 61 daily step-count observations from March–April 2026, including descriptive statistics, weekday patterns, autocorrelation, and STL decomposition.
2. **Microgrid energy forecasting:** Analysis and hourly forecasting of the `load_demand` variable using Holt-Winters exponential smoothing, SARIMA, and Prophet.

**Goal:** Examine temporal patterns and compare traditional forecasting techniques on a common chronological test period.

**Data:** The step-count series was derived from a personal Apple Health export; neither the original health export nor the step-count CSV is included in this repository. The microgrid data are attributed in the project report to [Colabsss — Microgrid Energy Forecasting Dataset (Kaggle)](https://www.kaggle.com/datasets/colabsss/microgrid-energy-forecasting-dataset). Check the source's terms before obtaining or redistributing the data. The original dataset is also omitted from this repository.

## Methodology

1. **Step-count EDA:** Summarize daily steps and inspect outliers, weekday differences, lag relationships, autocorrelation, rolling statistics, stationarity, and seasonality
2. **Energy data preparation:** Read 15-minute microgrid measurements and aggregate numeric variables to hourly means
3. **Exploratory analysis:** Inspect hourly demand patterns, ACF/PACF, STL decomposition and the Augmented Dickey–Fuller test
4. **Chronological split:** Use the earliest 80% of hourly observations to train and the last 20% (290 hourly observations) to evaluate the forecasts
5. **Forecasting models:** Fit additive Holt-Winters (daily seasonality), SARIMA `(1,1,1) × (1,0,1,24)`, and Prophet with daily and weekly seasonality
6. **Evaluation:** Compare MAE, MSE and RMSE on the same held-out period and inspect residuals

The analysis is implemented in [`Forecasting_SS26_part1-and-part2.ipynb`](Forecasting_SS26_part1-and-part2.ipynb). To run it, install the libraries from `requirements.txt` and place `schritte_tageswerte.csv` and `microgrid_energy_dataset.csv` alongside the notebook. **These source datasets are not provided here.**

## Results

The following figures are **saved notebook results**, not independently reproduced in this portfolio preparation. Values refer to the held-out hourly microgrid energy-demand test set.

| Model | Test MAE | Test MSE | Test RMSE |
|---|---:|---:|---:|
| Holt-Winters | 84.3449 | 11193.4492 | 105.7991 |
| SARIMA | 84.3087 | **11024.6266** | **104.9982** |
| Prophet | **83.8774** | 11027.3574 | 105.0112 |

**Comparison:** SARIMA had the lowest test RMSE, while Prophet had the lowest MAE. Their scores were very close; this single test split is not sufficient to establish a generally superior forecasting method.

## Interpretation and Limitations

- The personal step-count series is short (61 days) and is not representative of other individuals; measurements depend on carrying the phone.
- The microgrid evaluation uses one chronological 80/20 split, not rolling-origin backtesting or external validation.
- The energy forecast is **univariate**: models predict `load_demand` from its history without incorporating potential external predictors.
- Model comparisons should consider multiple metrics and temporal validation, not just the lowest reported error.
- The notebook's stored execution outputs were cleared for the portfolio copy; the metrics above were transcribed from the original saved outputs.
