# Bayesian Ridge Regression for Predicting Climate and Anxiety

**Authors:** Dishi Arun, John Black, Norah O'Callaghan, Rutva Doshi, Suvan Pattanaik

## Overview

Extreme heat is increasingly linked to adverse mental health outcomes, particularly anxiety-related emergency department (ED) visits. This project presents a multi-output **Bayesian Ridge Regression (BRR)** model that jointly predicts climate variables and anxiety-related ED visit trends across five major U.S. cities, demonstrating a potential early-warning approach for public health preparedness.

Current public health systems remain largely reactive and focused on physical health outcomes, with few early-warning frameworks that incorporate mental health indicators alongside climate data. This project addresses that gap.

## Goals

1. **Joint predictive modeling.** Build a multi-output model that predicts both anxiety-related ED visit rates and climate variables from a shared feature set, filling a gap in existing literature where these are modeled separately.
2. **Regional robustness.** Evaluate the model across five geographically and climatically distinct U.S. cities — San Francisco, Los Angeles, Atlanta, Chicago, and New York — representing Northern California, Southern California, the Southeast, the Midwest, and the Northeast.

## Data Sources

- **[NA-CORDEX](https://na-cordex.org/)** (North American domain of the Coordinated Regional Climate Downscaling Experiment): daily climate variables (2000–2025) including max/min near-surface air temperature, surface downwelling shortwave radiation, surface pressure, precipitation rate, and near-surface wind speed, spatially extracted for the five target cities via nearest-neighbor grid lookup and aggregated to monthly means.
- **CDC / National Syndromic Surveillance Program (NSSP):** monthly anxiety-related ED visit rates (per 100,000 visits), stratified by age group (12–17, 18–34, 35–64, 65+), covering January 2019–2025.

After alignment, the harmonized dataset spans **83 continuous months** across both sources.

## Methodology

- **Model:** Bayesian Ridge Regression (scikit-learn), chosen over deep learning approaches (LSTM, Transformer) due to the small dataset size (83 months) — BRR offers strong performance on limited data while preserving interpretable, explicit coefficient weights, which matters for public-health decision-making.
- **Feature engineering:** Month was cyclically encoded via sine/cosine transforms to correctly capture the annual seasonality of both climate and anxiety trends (a linear month encoding failed to generalize into future forecasts).
- **Train/test split:** ~70/30 (72/28), chronological — trained on the first 5 years, tested on the remaining 2 years, to evaluate real forecasting validity rather than random cross-validation.
- **Evaluation metric:** Mean Absolute Percentage Error (MAPE), chosen over MAE/MSE/RMSE because model outputs span vastly different scales (precipitation ~<1 unit vs. anxiety visit rates in the thousands).
- **Hyperparameter tuning:** alpha, lambda, tolerance, and max iterations were swept across multiple orders of magnitude to evaluate robustness; default scikit-learn values performed best for nearly all variables.

## Key Results

- **Anxiety ED visit prediction:** test MAPE of **12.54%**, competitive with LSTM-based approaches in the literature despite using a far smaller (83-month), non-institution-specific dataset.
- **Solar radiation** showed the strongest and most stable correlation with anxiety outcomes across all five cities (MAPE consistently below 10%, best in Los Angeles at ~4%).
- **Surface pressure** predictions were highly accurate and stable across cities (MAPE range: 0.08%–0.16%).
- **Precipitation** was the least predictable variable, with MAPE inflated by near-zero true values (a known limitation of MAPE under zero-inflated data).
- The model captured the cyclical, seasonal nature of anxiety incidence (higher in summer months) and produced reasonable 2026–2028 forecasts, though it noticeably over-predicts recent trends — likely an artifact of COVID-19-era anxiety spikes present in the training data.

See the full paper (`Bayesian_Ridge_Regression_for_Predicting_Climate_and_Anxiety.pdf`) in this repo for complete methodology, figures, and discussion.

## Repository Structure

> _Update this section to match the actual folder layout of the repo._

```
├── data/                # Raw and processed climate/anxiety datasets
├── notebooks/           # Analysis and modeling notebooks
├── src/                 # Model training / preprocessing scripts
├── figures/             # Generated plots and visualizations
├── Bayesian_Ridge_Regression_for_Predicting_Climate_and_Anxiety.pdf
└── README.md
```

## Getting Started

> _Update the commands below to reflect how the code is actually run (script vs. notebook, dependencies, etc.)._

```bash
git clone https://github.com/rdoshi7578/Bayesian-Ridge-Regression-Model-for-Predicting-Climate-and-Anxiety.git
cd Bayesian-Ridge-Regression-Model-for-Predicting-Climate-and-Anxiety
pip install -r requirements.txt
```

### Dependencies

- Python 3.x
- scikit-learn
- pandas / numpy
- matplotlib
- netCDF4 (for reading NA-CORDEX data)

## Limitations

- The combined dataset is limited to 83 months due to the shorter availability window of CDC mental health data (2019–2025).
- CDC anxiety data is nationally averaged rather than regionally resolved, so the model cannot currently produce region-specific anxiety forecasts.
- Training data includes the COVID-19 pandemic period, which appears to inflate the model's anxiety forecasts for 2026–2028.

## Future Work

- Retrain on post-pandemic-only data to reduce COVID-era distortion.
- Incorporate state- or county-level mental health data to resolve the spatial mismatch with high-resolution climate data.
- Explore LSTM or other sequence models as more regionally granular data becomes available, to better capture seasonal lag effects.

## Citation

If you use this work, please cite:

> Arun, D., Black, J., O'Callaghan, N., Doshi, R., & Pattanaik, S. "Bayesian Ridge Regression for Predicting Climate and Anxiety." Georgia Institute of Technology, 2026.

## Demo

A mockup GUI demonstration is available here: [https://youtu.be/nc81qrzeqRc](https://youtu.be/nc81qrzeqRc)
