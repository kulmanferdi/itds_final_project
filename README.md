# Introduction to data science final project

## Project Overview

This repository contains three regression-based experiments showcasing the performance of various models on analytical functions, synthetic datasets, and real-world weather data.


[Github](https://github.com/kulmanferdi/itds_final_project)  

**Tasks:**
1. Univariate Regression on Analytical Functions
2. Synthetic Regression Dataset Evaluation
3. Weather Time Series Forecasting

---

## Task 1: Regression on Mathematical Functions

### How to solve

We built and split function-based datasets, tested various regression models, engineered features for better performance, and evaluated models on both clean and noisy data.

### Dataset

- My functions:
  - `f₁(x) = x·sin(x) + 2x`
  - `f₂(x) = 10·sin(x) + x²`
  - `f₃(x) = sign(x)·(x² + 300) + 20·sin(x)`
- 100 samples in the interval `[-20, 20]`
- Train/Test split: 70% / 30%

### Model Performance

#### ▶ f₁(x)

| Model         | R² Score | Comment                      |
|---------------|----------|------------------------------|
| Linear/Ridge  | ~0.89    | Decent, but misses curvature |
| SVR (RBF)     | 1.00     | Perfect nonlinear fit        |
| Random Forest | 0.99     | Strong generalization        |
| MLP Regressor | ~0.89    | Likely underfitting          |

#### ▶ f₂(x)

| Model         | R² Score | Comment                      |
|---------------|----------|------------------------------|
| Linear/Ridge  | -0.30    | Poor for nonlinear patterns  |
| SVR (RBF)     | 1.00     | Excellent fit                |
| Random Forest | 1.00     | Captures both components     |
| MLP Regressor | 0.99     | Minor error                  |

#### ▶ f₃(x)

| Model         | R² Score | Comment                      |
|---------------|----------|------------------------------|
| Linear/Ridge  | ~0.93    | Surprisingly strong          |
| SVR (RBF)     | 0.94     | Robust nonlinear fit         |
| Random Forest | 1.00     | Best performing              |
| MLP Regressor | 0.99     | Nearly perfect               |

### Feature Engineering

| Function | Feature Type         | Best R² | Comment                          |
|----------|----------------------|--------|----------------------------------|
| f₁       | Trigonometric         | 0.99   | Matches sinusoidal behavior      |
| f₂       | Polynomial            | 0.99   | Captures quadratic growth        |
| f₃       | Trig + Polynomial     | 1.00   | Combines all relevant components |

---

## Task 2: Synthetic Regression Dataset Evaluation

### How to solve

We created a dataset to simulate car value estimation, evaluated various regression techniques on it, and then made the dataset more challenging to test model robustness.

### Dataset Variants

- **Standard:** 20 informative features, no noise  
- **Hard:** 15 informative + 5 redundant features, high noise (50)

### Model Results

Code fails to compile.

---

## Task 3: Weather Time Series Forecasting

### How to solve

We used a WWII weather dataset and explored it to check its initial values. For now, we only had to focus on data from one sensor. Using a window function, we predicted the 8th day from the previous 7, then trained, evaluated, and compared four prediction models.

### Data Setup

- **Source:** `SummaryofWeather.csv`
- **Station Selected:** 22508
- **Target Variable:** `MeanTemp`
- **Preprocessing Steps:**
  - Removed missing temperature values
  - Created 7-day rolling input windows to predict temperature **2 days ahead**
  - Split:
    - **Training set:** All data before 1945
    - **Test set:** Data from the year 1945

---

### Model Performance

**Linear Regression:** R2 = 0.6797, MSE = 0.7436  
**Random Forest:** R2 = 0.6369, MSE = 0.8430  
**Neural Network:** R2 = 0.6468, MSE = 0.8199  

#### Tuned Random Forest

- **Hyperparameters adjusted:**
  - `n_estimators`
  - `max_depth`
  - `min_samples_split`
- **Post-tuning performance:**
  - **R²:** 0.7195
  - **MSE:** above 13k, probably not correct

---

### Insights & Observations

- **Linear Regression** outperformed other models by capturing long-term trends effectively.
- **Random Forest** initially struggled but improved significantly with proper tuning.
- **MLP Regressor** showed potential but faced instability, likely due to limited data and lack of extensive tuning.
- Overall, simpler models proved more robust for this low-variability, historical time series data.

---

### Visualization Summary

- Linear regression lines closely followed the general temperature trend but missed short-term variations.
- Random Forest (after tuning) captured some short-term patterns better, although it was more sensitive to noise.

### In general... 

The predicted and actual series are similar if the model performs well, with the predicted curve closely tracking the actual data. While linear regression can capture short-term seasonality and local trends, it struggles with long-term patterns unless specifically engineered. Additionally, since it only predicts one step ahead, multi-step forecasting requires feeding predictions back into the model, which can lead to compounding errors. For better long-horizon forecasting, sequence models like RNNs or LSTMs are more effective.

--- 
**Author:** Ferdinand Kulman  
**Neptun ID:** YR9905   
