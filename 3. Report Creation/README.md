# Gold Market Modeling Report  
**Insights Presentation**

This report visualizes and explains the relationship between global financial markets and gold prices using daily data from 2010 to 2019. Each dashboard page is designed to reveal dynamic patterns between gold, equities, energy, and currencies, and how these factors influence the EUR/USD exchange rate. The Power BI report can be filtered by year and asset for deeper inspection.

📊 **Link to the Interactive Power BI Report**: [Report]

📌 **Disclaimer**: This report uses currency and date formats based on EN-US regional settings. If viewing outside of this locale, please adjust your browser settings accordingly to ensure consistent units and formats.

---

## Overview

This page gives a bird’s-eye view of market performance and correlations:

- **Key Metrics**: Displays daily price averages, percentage volatility, and EUR/USD prediction error using regression models.
- **Gold vs EUR/USD Trendlines**: Visualizes the co-movement and divergence of the two series, highlighting periods of strong correlation.
- **Cross-Market Price Correlations**: Matrix view of relationships between gold, oil, equities, and forex over time.
- **Price Distribution Histograms**: Spot anomalies and assess skewness of daily returns for each asset.

*Purpose*: Quickly understand which markets are most strongly aligned with gold movements and how this impacts FX.

---

## Gold Price Drivers

This page isolates factors that influence gold price movements:

- **Feature Importance (XGBoost)**: Ranked display of variables like SPX, USO, and EUR/USD and their predictive contribution.
- **Gold vs SPX vs USO**: Multi-axis plot showing inverse correlation with equities and partial correlation with energy.
- **Time-Lagged Effects**: Scatter plots of lagged SPX/USO changes vs current GLD price—helpful for short-term trading insights.
- **Outlier Impact Analysis**: Highlights how extreme equity or oil shocks impact gold volatility.

*Purpose*: Understand the behavioral and economic variables most closely associated with gold ETF pricing.

---

## EUR/USD Forecasting

This page highlights the FX modeling process:

- **Predicted vs Actual EUR/USD**: Comparison charts for each model (Random Forest, XGBoost, Lasso Polynomial).
- **R² & MAE Metrics by Model**: Evaluates how each algorithm performed on test data.
- **Residual Analysis**: Displays prediction errors across time—detects periods where the model under/over-predicts.
- **Model Tuning Parameters**: View of hyperparameters used (e.g., depth for trees, alpha for Lasso).

*Purpose*: Show the predictive strength of gold, equities, and oil when modeling EUR/USD, and explain model accuracy visually.

---

## Trend Insights by Year

This page breaks down year-over-year behavior:

- **Annual Average Price Comparison**: Bar charts comparing GLD, SPX, USO, and EUR/USD by year.
- **Macro Events Overlay**: Annotated timelines (e.g., 2011 Euro Crisis, 2014 Oil Crash).
- **Yearly Gold–Forex Correlation**: Demonstrates changing relationships in risk-on vs risk-off periods.
- **Volatility Bands**: Standard deviation bands overlaid on price lines to assess stability.

*Purpose*: Reveal how external economic shocks influence gold behavior and test if asset correlations remain stable.

---

## Model Deployment Readiness

This technical page outlines deployment scenarios:

- **Model Export Options**: Shows serialization methods (e.g., Pickle, ONNX) for the best-performing model.
- **API Design Blueprint**: Diagram of a REST-based endpoint that takes real-time SPX/GLD/USO values and returns EUR/USD forecasts.
- **Error Monitoring Dashboard**: Prototype for tracking live prediction error and confidence bounds.
- **Next Feature Ideas**: Includes macroeconomic data (VIX, CPI, bond yields) for model enrichment.

*Purpose*: Translate research models into production-ready tools for financial analysts and data scientists.

---

## Actionable Insights

| Insight | Strategic Implication |
|--------|------------------------|
| Gold prices are **strongly correlated** with EUR/USD (~0.76) | Traders may use gold trends as leading signals in forex markets |
| Equity indices (SPX) have a **negative relationship** with gold | Reinforces gold’s role as a safe-haven during market declines |
| XGBoost delivers the **most accurate FX predictions** | Ideal model choice for low-latency forecasting pipelines |
| Oil prices have **limited influence** | Energy is a secondary driver; focus on FX and equity for gold analysis |
| Polynomial models highlight **nonlinear interactions** | Suggests relationships are not purely linear and require advanced feature construction |

---
*Report generated based on `gold.ipynb`, built using Power BI on July 14, 2025.*

