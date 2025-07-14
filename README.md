# Gold Price & Market Interaction Project – Summary Report

## Description

This project explores the relationship between **gold prices** (as tracked by the GLD ETF) and several macro-financial indicators, namely:

- **S&P 500 (SPX)**: Equity market proxy  
- **US Oil Fund (USO)**: Energy commodity proxy  
- **EUR/USD**: Euro to US Dollar exchange rate (used as **target variable**)  

The goal is to uncover the underlying drivers of gold prices and evaluate the **predictive capability of gold, oil, and equities** in estimating forex movements, using advanced machine learning techniques.

**Data Source**: Public market datasets (2010–2019)

---

## Objectives

The core objectives of this project are:

- **Understand cross-asset relationships**  
  Identify how gold correlates with equities, energy, and currency markets across economic regimes.

- **Model EUR/USD using market features**  
  Build predictive models to forecast the EUR/USD rate using gold, oil, and equity data.

- **Benchmark Machine Learning Models**  
  Compare performance across Random Forests, Lasso Regression, and XGBoost.

- **Create actionable visualizations**  
  Design an interactive Power BI dashboard to communicate findings clearly.

**Personal Development Goals**:
- Practice data cleaning with `pandas`, statistical modeling using `sklearn` and `xgboost`.  
- Apply winsorization, scaling, feature selection, and SHAP value interpretation.  
- Develop end-to-end modeling pipelines suitable for deployment.

---

## Project Phases

### 1. Data Preparation
- Loaded and cleaned daily price data for GLD, SPX, USO, SLV, and EUR/USD.
- Dropped SLV due to high collinearity with gold.
- Imputed missing values using means.
- Applied **5th/95th percentile capping** to handle outliers.
- Standardized numerical features using `StandardScaler`.

### 2. Exploratory Analysis
- Gold is **strongly correlated** with EUR/USD (ρ ≈ 0.76).
- Gold has **inverse correlation** with SPX (ρ ≈ –0.42), confirming its safe-haven status.
- Oil shows **moderate positive correlation** with gold and FX.
- Detected structural shifts: e.g., post-2014 oil collapse, Eurozone crises, and 2018 USD appreciation.

### 3. Modeling & Forecasting
- Built three models to predict EUR/USD:
  - **Random Forest Regressor**
  - **Polynomial Regression + Lasso (deg=2)**
  - **XGBoost Regressor**

| Model | R² Score | MAE |
|-------|----------|-----|
| Random Forest | 0.86 | 0.0034 |
| Lasso Polynomial | 0.88 | 0.0032 |
| **XGBoost** | **0.92** | **0.0026** |

- XGBoost was the top performer due to its ability to handle non-linear interactions.
- Residuals were homoscedastic and normally distributed—confirming model validity.

### 4. Report Creation
- Built a multi-page Power BI dashboard:
  - **Overview**: Asset trends, correlations, volatilities.
  - **Gold Drivers**: Feature importance, lag analysis.
  - **EUR/USD Modeling**: Model scores, prediction vs actual.
  - **Annual Trends**: Economic events, regime shifts.
  - **Deployment Readiness**: REST API mock-up, SHAP insights.

---

## Key Findings

- **GLD is a leading indicator** of EUR/USD movement. Price uptrends in gold are often matched by Euro strength.
- **SPX (stocks)** are inversely related to gold. Gold demand rises during equity sell-offs.
- **XGBoost outperforms** all other models in both accuracy and interpretability.
- **Oil prices (USO)** play a secondary role but can still complement FX models.

---

## Recommendations

- **For Traders**: Use GLD momentum to guide EUR/USD positioning.
- **For Analysts**: Track divergence between SPX and GLD for early macro signals.
- **For Modelers**: Extend the feature set to include macroeconomic indicators (e.g., CPI, yields).
- **For Deployment**: Serialize the XGBoost model and build a real-time API wrapper for dynamic FX forecasting.

---

*Prepared on July 14, 2025. Based on the `gold.ipynb` notebook and associated Power BI visualizations.*
