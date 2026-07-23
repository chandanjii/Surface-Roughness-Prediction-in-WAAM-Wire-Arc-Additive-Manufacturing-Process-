# Surface-Roughness-Prediction-in-WAAM-Wire-Arc-Additive-Manufacturing-Process-
# Predicting Surface Roughness in a WAAM Process

Comparing **Random Forest** and **K-Nearest Neighbors** regression models to predict the
surface roughness (Ra) of a deposited workpiece from three Wire Arc Additive Manufacturing
(WAAM) process parameters.

## Problem

In WAAM (Wire Arc Additive Manufacturing), surface finish quality (measured as average
roughness, `Ra`) depends on process settings. Being able to predict `Ra` from those settings
ahead of time helps choose parameters that produce a target finish without expensive
trial-and-error deposition runs.

## Dataset

27 experimental runs, each with:

| Parameter | Description |
|---|---|
| `TS` | Traverse Speed (mm/min) |
| `OCV` | Open Circuit Voltage (V) |
| `WFR` | Wire Feed Rate (m/min) |
| `Avg. Ra` | Average surface roughness (µm) — **target variable** |

## Approach

1. **EDA** — correlation heatmap and feature-vs-target scatter plots to check relationships before modeling.
2. **Train/test split** — a single split reused for both models so results are directly comparable.
3. **Random Forest Regressor** — baseline model, then tuned via `GridSearchCV` (3-fold CV) over `n_estimators`, `max_depth`, `min_samples_split`, and `min_samples_leaf`.
4. **KNN Regressor** — features scaled with `StandardScaler`; `k` chosen by evaluating a small range of candidates rather than a fixed guess.
5. **Evaluation** — both models scored with R² and MSE on the same held-out test set.

### Exploratory data analysis

![Correlation heatmap](images/correlation_heatmap.png)

![Surface roughness vs. each process parameter](images/feature_vs_target.png)

### Choosing k for KNN

![KNN k selection](images/knn_k_selection.png)

## Results

| Model | R² | MSE |
|---|---|---|
| Random Forest | `[0.930]` | `[0.0871]` |
| KNN (k=`[6]`) | `[0.884]` | `[0.1430]` |

![Actual vs predicted surface roughness](images/actual_vs_predicted.png)

*(Note: with only 27 samples, these results are a proof-of-concept comparison rather than a
statistically robust conclusion — a larger dataset would be needed to generalize further.)*


## Tools

Python · pandas · scikit-learn · seaborn · matplotlib
