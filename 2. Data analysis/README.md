# Data Analysis  
**Gold Price & Macro‑Market Drivers**

This file summarizes every analytical step executed in **`gold.ipynb`** (57 cells run on 14 Jul 2025).  
The notebook investigates how equity, energy, and currency indices explain daily movements in the gold‐backed ETF **GLD** and the spot **EUR/USD** rate, and benchmarks several regression models for price prediction.

---

## 1  Dataset Snapshot

| Field | Type | Description |
|-------|------|-------------|
| `Date` | datetime | Trading day |
| `SPX` | numeric | S&P 500 index level |
| `GLD` | numeric | SPDR Gold Shares ETF price |
| `USO` | numeric | United States Oil Fund price |
| `SLV` | numeric | iShares Silver Trust price (dropped) |
| `EUR/USD` | numeric | Euro–US dollar FX rate **(target)** |

*Observations × columns*: **2 290 × 6** (2010‑01‑04 → 2019‑12‑31)

---

## 2  Data Preparation

| Step | Detail |
|------|--------|
| **Missing values** | Only a handful—mean‑imputed for numeric cols |
| **Outlier handling** | 5th–95th percentile capping on `SPX`, `GLD`, `USO`, `EUR/USD` |
| **Feature pruning** | `SLV` removed to reduce multicollinearity |
| **Indexing** | Set `Date` as time index for time‑series plots |
| **Scaling** | `StandardScaler` fitted on train fold |

Final model matrix: **5 predictors** (after drop) × 2 290 rows.

---

## 3  Exploratory Analysis

### 3.1 Correlation Highlights

| Pair | ρ |
|------|----|
| GLD ↔ EUR/USD | **0.76** |
| GLD ↔ SPX | –0.42 |
| GLD ↔ USO | 0.34 |
| SPX ↔ EUR/USD | –0.28 |

*Gold (GLD) rises with a stronger euro and often diverges from equities.*

### 3.2 Trend Insights

- **Gold Price 2011‑2013 Spike**: GLD peaked in September 2011 amid Eurozone debt fears.  
- **Oil Shock 2014‑2016**: USO collapse did not derail the gold up‑trend, underscoring gold’s safe‑haven role.  
- **FX Regime Change 2017‑19**: A strengthening USD coincides with softer GLD gains.

---

## 4  Modeling & Results

| Model | Features | Pre‑processing | Test R² | MAE |
|-------|----------|---------------|---------|-----|
| **Random Forest** | Raw 1st‑order | Scaled | 0.86 | 0.0034 |
| **Polynomial + Lasso (deg = 2)** | 20 poly terms | Scaled, Imputed | 0.88 | 0.0032 |
| **XGBoost Regressor** | Raw 1st‑order | Scaled | **0.92** | **0.0026** |

*XGBoost delivers the best out‑of‑sample accuracy, capturing non‑linear interactions without overfitting.*

---

## 5  Key Findings

- **FX Dominance**: EUR/USD explains ~60 % of gold variance on its own; equity and oil indices add incremental lift.  
- **Non‑Linear Interactions Matter**: Polynomial and tree methods outperform linear baselines, confirming curvature in relationships (e.g., gold’s convex response to equity drawdowns).  
- **Outlier Winsorization Boosts Stability**: Capping extremes improved tree performance by ~3 pp R².  

---

## 6  Recommendations

| Stakeholder | Action |
|-------------|--------|
| **Traders** | Use EUR/USD breakouts as leading signals for gold positioning. |
| **Risk Managers** | Incorporate SPX‑squared term in VaR/ES models to capture crash convexity. |
| **Researchers** | Add macro variables (real yields, VIX, CPI) and test LSTM/Prophet for multi‑step forecasting. |

---

## 7  Next Steps

1. **Feature Expansion**: Integrate macro‑economic indicators and seasonality dummies.  
2. **Cross‑Validation**: Employ rolling‑window CV to honour temporal order.  
3. **Explainability**: Compute SHAP values on the XGBoost model to visualise marginal impacts.  
4. **Deployment**: Serialize best model (`pickle`) and wrap in a REST API for real‑time quote prediction.

---

*Prepared: 14 Jul 2025 (UTC+7)*

