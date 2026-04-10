# ARIMA-GARCH Volatility Analysis: Coca-Cola (KO) & PepsiCo (PEP) 📈

**RMIT University | Master of Finance | Financial Econometrics (ECON-1195)**  
**Submitted:** September 2025 | **Grade:** Distinction

---

## Overview

This project models the **mean return dynamics and conditional volatility** of Coca-Cola (KO) and PepsiCo (PEP) using daily stock returns from **2019 to 2024** (1,305 trading days). It extends a prior Fama-French factor analysis by applying advanced econometric techniques — ARIMA for mean dynamics and GARCH-family models for volatility — that simple regressions cannot fully capture.

---

## Research Objectives

- Model mean return dynamics using the **Box-Jenkins ARIMA framework**
- Select best-fit ARIMA specification using **AIC, BIC, and Ljung-Box diagnostics**
- Test for **volatility clustering and ARCH effects** in both return series
- Compare **sGARCH(1,1), GJR-GARCH(1,1), and GARCH-M(1,1)** specifications
- Determine whether **risk premiums are embedded** in daily returns via ARCH-in-mean term
- Draw **investment implications** from volatility and risk profiles of both stocks

---

## Tools & Libraries

| Tool | Purpose |
|------|---------|
| **R / RStudio** | All statistical modelling and diagnostics |
| `forecast` | ARIMA model estimation and selection |
| `rugarch` | GARCH-family model estimation |
| `tseries` | Stationarity and ARCH effect testing |
| `PerformanceAnalytics` | Return calculation and performance metrics |
| `ggplot2` | Data visualisation |
| **Investing.com** | Daily adjusted closing price data (2019–2024) |

---

## Methodology

### Stage 1 — ARIMA Modelling (Mean Return Dynamics)

Daily adjusted closing prices transformed into **continuously compounded logarithmic returns**.  
Stationarity confirmed via `ndiffs()` → d = 0 for both series.

**4 ARIMA specifications evaluated per stock:**

| Model | Rationale |
|-------|-----------|
| ARIMA(1,0,1) | Minimalist baseline — one-day AR and MA shock |
| ARIMA(2,0,2) | Matches clear 1–2 day signal in ACF/PACF |
| ARIMA(4,0,3) | Medium-lag AR flexibility with richer MA |
| ARIMA(5,0,2) | Captures 5-day PACF activity, compact MA |

**Selection criteria:** Lowest AIC/BIC + Ljung-Box p > 0.005 at lags 10 and 20

#### KO — ARIMA Results

| Model | AIC | BIC | LB p(10) | LB p(20) | Decision |
|-------|-----|-----|----------|----------|----------|
| **ARIMA(2,0,2)** | **3387.792** | **3416.679** | 0.0349 | 0.1689 | ✅ **Selected** |
| ARIMA(5,0,2) | 3391.419 | 3434.750 | 0.0369 | 0.2011 | Second-best |
| ARIMA(4,0,3) | 3391.841 | 3435.172 | 0.0137 | 0.1916 | Second-best |
| ARIMA(1,0,1) | 3397.592 | 3416.850 | 0.0026 | 0.0173 | ❌ Rejected |

#### PEP — ARIMA Results

| Model | AIC | BIC | LB p(10) | LB p(20) | Decision |
|-------|-----|-----|----------|----------|----------|
| **ARIMA(5,0,2)** | **3366.970** | **3410.301** | 0.0696 | 0.0886 | ✅ **Selected** |
| ARIMA(4,0,3) | 3372.722 | 3416.053 | 0.0007 | 0.0104 | ❌ Rejected |
| ARIMA(1,0,1) | 3378.012 | 3397.271 | 0.0037 | 0.0041 | ❌ Rejected |
| ARIMA(2,0,2) | 3381.731 | 3410.618 | 0.0009 | 0.0016 | ❌ Rejected |

---

### Stage 2 — GARCH Modelling (Volatility Dynamics)

Built on respective ARIMA mean models. Three GARCH specifications tested:

1. **sGARCH(1,1)** — standard model, volatility depends on yesterday's shocks and variance
2. **GJR-GARCH(1,1)** — asymmetric model, captures leverage effects (bad news > good news)
3. **GARCH-M(1,1) with Student-t** — allows volatility to influence returns directly; handles fat tails

#### KO — GARCH Results

| Model | LogLik | AIC | BIC | LB(10) | ARCH LM p | Decision |
|-------|--------|-----|-----|--------|-----------|----------|
| sGARCH(1,1) | -1591.961 | 3.5191 | 3.5773 | 0.9773 | 0.7859 | Adequate |
| GJR-GARCH(1,1) | -1604.835 | 3.5496 | 3.6130 | 0.6851 | 0.8245 | Adequate |
| **GARCH-M(1,1) — t** | **-1449.293** | **3.2103** | **3.2790** | 0.4999 | 0.8872 | ✅ **Selected** |

#### PEP — GARCH Results

| Model | LogLik | AIC | BIC | LB(10) | ARCH LM p | Decision |
|-------|--------|-----|-----|--------|-----------|----------|
| sGARCH(1,1) | -1554.491 | 3.4369 | 3.4950 | 0.9759 | 0.9517 | Adequate |
| GJR-GARCH(1,1) | -1553.800 | 3.4375 | 3.5010 | 0.9579 | 0.9438 | Adequate |
| **GARCH-M(1,1) — t** | **-1420.172** | **3.1464** | **3.2151** | 0.8337 | 0.7345 | ✅ **Selected** |

---

## Key Findings

| | Coca-Cola (KO) | PepsiCo (PEP) |
|--|----------------|---------------|
| **Best ARIMA** | ARIMA(2,0,2) | ARIMA(5,0,2) |
| **Best GARCH** | GARCH-M(1,1) — Student-t | GARCH-M(1,1) — Student-t |
| **Volatility Profile** | Defensive, lower persistence | Higher volatility, stronger risk premium sensitivity |
| **Leverage Effects** | No strong evidence | No strong evidence |
| **Investment Role** | Stable core holding | Tactical, value-oriented opportunity |

- Both stocks exhibit **volatility clustering** — calm periods followed by turbulent bursts
- **GARCH-M(1,1) Student-t** confirmed fat-tailed return behaviour and **embedded risk premiums** in daily returns
- No long-run return predictability found — consistent with **Efficient Market Hypothesis**

---

## Investment Implications

- 🛡️ **Conservative investors** → Prefer **Coca-Cola (KO)** for defensive, low-volatility exposure
- 📊 **Value-oriented investors** → Consider **PepsiCo (PEP)** for tactical opportunities in consumer staples
- ⚠️ **Risk managers** → Monitor conditional variance forecasts; clustering effects imply rapid risk escalation
- 🔬 **Future research** → Extend to intraday data or macroeconomic linkages for deeper forecasting

---

## Repository Structure

```
├── FE_Assignment_2_s4103956.pdf   # Full research report
├── KO_PEP_ARIMA_GARCH.R           # Main R analysis script
└── README.md                      # Project documentation
```

---

## References

- Engle, R.F. (1982). Autoregressive conditional heteroscedasticity
- Bollerslev, T. (1986). Generalized autoregressive conditional heteroscedasticity
- Box, G.E.P. & Jenkins, G.M. — Time Series Analysis
- Akaike, H. (1974). AIC information criterion
- Schwarz, G. (1978). BIC criterion

---

*RMIT University — Master of Finance | Financial Econometrics ECON-1195*
