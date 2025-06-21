# Gold Price Predictor: Integrating Market Dynamics and Machine Learning

##  Project Overview
This project aims to forecast the **direction of gold price movement (up/down)** using **machine learning techniques** and a diverse set of financial and macroeconomic indicators. The model integrates time series feature engineering, classification algorithms, and data rebalancing strategies to capture the complex dynamics driving gold prices.

---

##  Data Sources
Data was collected using the `yfinance` Python library, retrieving daily prices and indices:

- **Gold Prices (USD/oz)**
- **USD/INR Exchange Rate**
- **10-Year US Treasury Yield**
- **S&P 500 Index**
- **VIX (Volatility Index)**
- **Crude Oil Prices**
- **Silver Prices**
- **Bitcoin Prices**

---

##  Economic Justification for Features

- **USD/INR**: Gold is imported to India in dollars, so a weak rupee makes gold costlier, reducing demand, while a strong rupee lowers prices, boosting affordability and purchases. That shows a positive correlation between the two factors.
- **10Y Yield**: 3. The traditional inverse link between bond yields and gold has weakened during this period of extraordinary geopolitical and economic uncertainty. Markets are now highly reactive to:
* Central bank policy decisions.
* Shifting geopolitical alliances.
* Stock market performance.
* Trade disruptions. This combination is likely to sustain volatility in both gold and bond markets through 2025 and beyond.
- **S&P 500**: Recent analysis from Goldman Sachs shows that gold and stock market has maintained an average -0.43 correlation to the S&P 500 during periods of high inflation since 1971, highlighting this inverse relationship during key economic stress points.
- **VIX**: When the VIX index increases, the volatility of the market is expected to increase in near term future periods and investors may exhibit flight-to-safety, flight-to-quality, and flight-to-liquidity behaviour. Thus, GLD ETFs and common equities related to the gold industry are expected to increase in value.
- **Crude Oil**: Crude oil prices generally have a positive impact on gold prices. Rising oil prices tend to increase inflation, and gold is often seen as a safe-haven asset during inflationary periods, driving its price up. Additionally, increased oil prices can lead to economic uncertainty and instability, which also prompts investors to seek safe-haven assets like gold. 
- **Silver**: Silver and gold prices typically move together due to their shared characteristics as stores of value and safe-haven assets.
- **Bitcoin**: From November 2022 to November 2024, gold and bitcoin moved in a relatively tight correlation, with gold gaining 67% while the more volatile bitcoin surged nearly 400%. Analysts widely believed that the two assets would continue to move in tandem, given their shared status as hedges against weak global currency policies. However, this relationship began to fray in 2025. As of late March, gold has risen 16%, while bitcoin has fallen by more than 6%.


**Excluded Features**:
- **Import Duty**: Import tariffs is not considered in the project as you can see in the below table there are only few changes in the import duties over the past 10 years hence it may not be significant in our study.
- **GST**: The Goods and Services Tax (GST) on gold in India has remained consistent at 3% on the value of gold since the implementation of GST in 2017. This rate applies to all forms of gold, including jewellry, bars, and coins. Additionally, a 5% GST is applied on the making charges for gold jewellry. Since the value has no change since its introduction to Indian economy in 2017, we will not be considering this factor in our study.

---

##  Feature Engineering

| Feature Type     | Examples                  | Purpose |
|------------------|---------------------------|---------|
| **Lag Features** | `gold_lag1`, `vix_lag3`   | Capture time dependencies |
| **Rolling Stats**| `gold_ma5`, `vix_std5`    | Smooth volatility, track momentum |
| **Returns**      | `log_return`              | Model relative price movements |
| **Ratios**       | `gold/silver`, `gold/oil` | Show relative asset behavior |
| **Volatility**   | `rolling std`             | Capture uncertainty/trend strength |

---

## ⚙ Modeling Approach

### 1. **Problem Framing**
- Reformulated regression into **binary classification**: Will gold price go **up (1)** or **down (0)** next day?

### 2. **Class Balancing**
- Used **SMOTE (Synthetic Minority Over-sampling Technique)** on training data to address class imbalance.

### 3. **Model Development**
- Compared:
  - **Random Forest**
  - **XGBoost Classifier**
- Performed **RandomizedSearchCV** for hyperparameter tuning.
- Metrics evaluated: `Accuracy`, `ROC AUC`, `Classification Report`, and `Confusion Matrix`.

### 4. **Feature Selection**
- Used **XGBoost Feature Importance** to select top 20 features (excluding SHAP for speed and simplicity).

---

##  Results Summary

| Stage                        | Metric                | Value |
|-----------------------------|------------------------|-------|
| **Baseline (XGBoost)**      | Accuracy               | ~46%  |
|                             | ROC AUC                | ~0.45 |
| **After Tuning**            | Accuracy               | ~44%  |
|                             | Improved class recall  | Yes   |
| **Post Feature Selection**  | Accuracy               | ~46%  |
|                             | Slight stability gain  | ✓     |

>  The model's predictive performance is limited due to the complexity of the gold market and daily-level volatility, but results show improvement in class balance and understanding of signal structure.

---


---

## Future Improvements
- Try **ensemble methods** or **LSTM/RNNs** for deeper temporal modeling.
- Integrate **macroeconomic events** or **news sentiment**.
- Use **probabilistic thresholds** instead of fixed 0.5 cutoff.

---

## Acknowledgements
- Yahoo Finance (`yfinance`) for data access
- Scikit-learn, XGBoost, Pandas, NumPy for modeling pipeline
- Domain references from Goldman Sachs, WGC, and other research papers

---

##  Author
*Developed by Neha Mathew*  | Finance + Data Science Enthusiast

