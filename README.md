# GBP/USD Currency Call Option Pricing via Black-Scholes-Merton

## Overview

This project builds a call option pricing model for the GBP/USD exchange rate. It first validates Geometric Brownian Motion (GBM) as the underlying price process across four lookback windows (1Y, 2Y, 5Y, 10Y) of historical data, then prices a 30-day call option using the **Black-Scholes-Merton (BSM)** closed-form formula, and finally compares the model's output against a real market-quoted option premium.

The project demonstrates applied quantitative finance methods using real market data retrieved directly from Yahoo Finance.

---

## What This Project Does

1. Downloads 10 years of daily GBP/USD historical data from Yahoo Finance.
2. Splits the data into four lookback windows — 1-year, 2-year, 5-year, and 10-year — used to estimate volatility and test model assumptions.
3. For each window, tests whether GBM is a reasonable model for the exchange rate by checking:
   - Normality of log returns (histogram + Q-Q plot, visual inspection)
   - No autocorrelation (Ljung-Box test)
   - Stationarity of log returns (Augmented Dickey-Fuller test)
   - Rolling volatility (30-day window, visual inspection for constant variance)
4. Prices a 30-day GBP/USD call option using the **Black-Scholes-Merton closed-form formula**, with volatility estimated from each lookback window.
5. Compares the model's calculated premium against a real call option premium quoted on Investing.com, and discusses the gap between model and market price.

---

## Methods Used

| Method | Purpose |
|--------|---------|
| Log-normal returns | Transform price data into a stationary process |
| Ljung-Box Test | Test for autocorrelation in returns |
| Augmented Dickey-Fuller (ADF) Test | Confirm stationarity of log returns |
| Q-Q Plot | Visual normality check |
| Rolling Volatility (30-day) | Visual check of the constant-variance assumption |
| Black-Scholes-Merton Model | Closed-form option pricing |

---

## Tech Stack

```
Python 3 | numpy | pandas | matplotlib | scipy | yfinance | statsmodels
```

---

## Project Structure

```
gbpusd-currency-call-option/
│
├── gbpusd_currency_call_option.ipynb   # Full analysis notebook
├── requirements.txt
├── LICENSE
├── .gitignore
└── README.md
```

---

## Installation

```bash
pip install -r requirements.txt
```

---

## Key Results

- Across all four lookback windows, log returns show no significant autocorrelation (Ljung-Box) and reject the null of a unit root (ADF), supporting stationarity — both consistent with GBM.
- Normality and constant variance were assessed visually (Q-Q plots and rolling volatility plots) rather than with a formal statistical test in this version.
- The Black-Scholes-Merton model's calculated premium ($0.17483) **overshoots** the real market-quoted premium ($0.15377) for a comparable 12-month option, meaning the model would currently overprice this option relative to the market.

---

## Limitations

- **Single risk-free rate:** the model uses one domestic interest rate (Bank of England rate) rather than the two-rate approach (domestic and foreign) that a full FX-specific pricing model would use. This is a simplification of standard equity-style Black-Scholes rather than a currency-specific formulation.
- **Fixed strike price:** the call options priced across all four horizons use a strike of 1.00, which has been deep in-the-money for most of the sample period given GBP/USD's historical range. This makes the calculated premiums track the spot rate closely and understates how much volatility differences between horizons actually affect option pricing.
- **Normality and homoskedasticity** are currently assessed by eye (Q-Q plot, rolling volatility chart) rather than backed by a formal statistical test like Shapiro-Wilk or Jarque-Bera.

---

## Concepts Demonstrated

- **Geometric Brownian Motion (GBM)** and its assumptions
- **Black-Scholes-Merton option pricing**
- **Statistical hypothesis testing** for financial model validation (Ljung-Box, ADF)
- **Model validation against real market data**

---

## Author

**Mohammad Osama Khan**
MSc Financial Economics — Otto-von-Guericke University Magdeburg
[LinkedIn](https://www.linkedin.com/in/mohammad-osama-khan-93233a191) | mohammad2.khan@st.ovgu.de
