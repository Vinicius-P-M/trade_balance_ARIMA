# 📉 Forecasting Brazil’s Trade Balance Using SARIMA/SARIMAX (1995–2025)

This project builds a time-series forecasting model for **Brazil’s net trade balance** using **SARIMA** and **SARIMAX** methods.  
The goal is to generate short-term projections while evaluating the model’s limits, especially under structural economic shocks.

---

## 📁 About the Data

The dataset used (`sarimadatacomplete.csv`) contains monthly values from **1995 to late 2025** and includes:

1. **Commodity Price Index (CPI)** — *Independent variable*  
   - Simple average of international prices for soy, petrol, corn and meat  
   - Measured in **USD / unit of weight**

2. **Balance of Trade (b_trade)** — *Dependent variable*  
   - Net trade balance in **USD millions**

3. **USD/BRL Exchange Rate (xchange_rate)** — *Independent variable*  
   - Monthly average buy-side rate

---

## 🔧 Step 1: Forecasting the Independent Variables

Before forecasting the trade balance, we need reliable future values of its predictors.

- CPI is forecasted using a **simpler univariate method**.  
- The same procedure is applied to the **USD/BRL exchange rate**.  
- Both are projected **6 months ahead**.

These predictions are later merged back into the main dataframe.

---

## 📈 Step 2: SARIMAX Forecast for Trade Balance

With CPI and exchange rate forecasts ready, the final stage is running the **SARIMAX model** on the trade balance series.

The process:

1. Fit SARIMAX to the historical series  
2. Input CPI + FX predictions into the exogenous regressors  
3. Generate the final **trade balance forecast**

---

## ⚠️ Model Issues Identified

Some limitations emerged:

1. **High error margin:**  
   The model’s **USD 2,128.34** RMSE is large relative to the scale of the series.  
   → Suggests significant unexplained variance.

2. **Poorly adjusted lags:**  
   Correlograms show issues at **lags 2, 5 and 11**.  
   → These could be manually corrected, but they hint at a deeper structural mismatch.

---

## 🧭 Main Hypothesis: Structural Break in 2025

By mid-2025, the U.S. imposed **new tariffs on Brazilian exports**, sharply reducing trade flows.  
This shock appears clearly in the dataset: a steep drop in the trade balance starting July–August.

**Why this matters:**  
Trade patterns adjust slowly. Reallocating exports to new markets creates **lagged dynamics** the model isn’t equipped to absorb in its current configuration.

This structural break likely explains:

- the high error  
- the problematic lags  
- the model’s difficulty in stabilizing predictions

---

## 🔚 Conclusion & Next Steps

This project reaches its end here — but a follow-up could tackle the structural break more rigorously by:

- Testing **regime-switching models**  
- Using **intervention analysis**  
- Introducing **dummy variables for tariff periods**  
- Applying **VAR or VECM** models with additional macro indicators

---
Feel free to open an issue or reach out!

