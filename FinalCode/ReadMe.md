# Bayesian Ridge Regression for Climate and Anxiety Predictions
-----
## Overview
Bayesian Ridge Regression for Climate and Anxiety Predictions is a forecasting model that allows users to generate regional predictions for 6 climate variable, as well as anxiety incidence. This model is unique in its simplicity and ability to predict both outputs.

## Outputs
### BRR notebook
+ Seasonal historical overlap of climate and anxiety disorders
+ Bayesian Ridge Regression for climate and anxiety disorder Forecast 
+ Anxiety disorder past and forecast
+ Average seasonal patterns of climate and anxiety disorders
+ Anomaly analysis of deviations from monthly climatology

### Parameter analysis notebook
+ BRR Hyperparameter Sensitivity
+ Train vs Test MAE — Hyperparameter Scatter

## How it works
### BRR notebook
1. Dataset inputs
    + CORDEX city-specific climate .csv
    + CDC mental health visit incidence .csv
2. Data processing
    + Average daily CORDEX data into monthly
    + Convert months to cyclical form through sine and cosine (these are the input features)
    + Pivot anxiety data to match weather data formatting
    + Combine anxiety and weather data into one array
3. BRR training and testing
    + Training: 2019-2023
    + Testing: 2024-2025
    + Performance metric is MAPE (with MAE as well for some plots)
4. BRR prediction

### Parameter analysis notebook
1. Dataset inputs
    + CORDEX city-specific climate .csv
    + CDC mental health visit incidence .csv
2. Data processing
    + Average daily CORDEX data into monthly
    + Convert months to cyclical form through sine and cosine (these are the input features)
    + Pivot anxiety data to match weather data formatting
    + Combine anxiety and weather data into one array
3. BRR training and testing
    + Training: 2019-2023
    + Testing: 2024-2025
    + Performance metric is MAPE (with MAE as well for some plots)
    + Dynamic ranges are tested for alpha, lambda, maximum iterations, and tolerance

## Accomplishments
This model predicts both climate variables and anxiety incidence rates with relatively low MAPE. This model is simple and fast, allowing for easy implementation. 

## Requirements
+ Pandas, numpy, matplotlib.pyplot, matplotlib.dates, matplotlib.gridspec, matplotlib.ticker, seaborn, linear_model from sklearn, mean_absolute_error from sklearn.metrics
+ Jupyter Notebook
