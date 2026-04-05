## About This Project
This report extends the Fama-French analysis of Coca-Cola (KO) and PepsiCo (PEP) 
by modelling time-series dynamics and conditional volatility of their daily stock 
returns from 2019 to 2024. Using the Box-Jenkins framework, KO was best described 
by ARIMA(2,0,2) and PEP by ARIMA(5,0,2) — both confirming short-run dependence 
but no long-run predictability, consistent with the Efficient Market Hypothesis.

For volatility, three GARCH-family models were tested — sGARCH(1,1), 
GJR-GARCH(1,1), and GARCH-M(1,1) with Student-t innovations. The GARCH-M(1,1) 
with Student-t outperformed both alternatives for KO (AIC: 3.2103) and PEP 
(AIC: 3.1464), capturing volatility clustering, fat-tailed return distributions, 
and a direct risk-return trade-off. No strong leverage asymmetry was found in 
either stock.

The conclusion confirms that Coca-Cola is the more defensive, stable asset with 
lower volatility persistence, while PepsiCo carries higher sensitivity to risk 
premiums and a more cyclical exposure profile. Conservative investors seeking 
steady returns may prefer KO, while those targeting tactical value opportunities 
within consumer staples may consider PEP. The GARCH-M(1,1) with Student-t is 
recommended as the preferred specification for ongoing volatility monitoring 
and portfolio stress testing for both stocks.

**Course:** Financial Econometrics (ECON1195) | Master of Finance | RMIT University  
**Submitted:** September 2025
