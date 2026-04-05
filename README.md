# ARIMA-GARCH Volatility Analysis: Coca-Cola & PepsiCo (2019–2024)

**Course:** Financial Econometrics (ECON1195) | Master of Finance | RMIT University

## Overview
Extends the Fama-French analysis by modelling time-series dynamics and 
conditional volatility of KO and PEP daily returns from 2019 to 2024 using 
ARIMA and GARCH-family models.

## Methods Used
- ARIMA modelling for mean return dynamics (Box-Jenkins framework)
- GARCH(1,1), GJR-GARCH(1,1), GARCH-M(1,1) for volatility dynamics
- Model selection via AIC/BIC and Ljung-Box diagnostic tests

## Key Findings

### ARIMA Results
| Company | Best Model | Decision |
|---|---|---|
| Coca-Cola (KO) | ARIMA(2,0,2) | Lowest AIC/BIC, passed all diagnostics |
| PepsiCo (PEP) | ARIMA(5,0,2) | Only model passing all diagnostics |

### GARCH Results
| Company | Best Model | AIC |
|---|---|---|
| Coca-Cola (KO) | GARCH-M(1,1) with Student-t | 3.2103 |
| PepsiCo (PEP) | GARCH-M(1,1) with Student-t | 3.1464 |

- GARCH-M with Student-t outperformed standard and GJR-GARCH for both stocks
- Both stocks show **volatility clustering** but limited leverage effects
- Coca-Cola is the more **defensive, stable** asset; PepsiCo shows higher risk-return sensitivity

## Tools & Packages
R — rugarch, forecast, tseries, PerformanceAnalytics

## Files
| File | Description |
|---|---|
| FE_Assignment_2_s4103956.pdf | Full research report |

## Institution
RMIT University — Master of Finance | Financial Econometrics (ECON1195)
