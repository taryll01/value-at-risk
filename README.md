# Value at Risk: Historical, Parametric and Monte Carlo

Compares three ways of measuring the **Value at Risk (VaR)** of a portfolio, then checks VaR against the most recent month of returns (Oct–Nov 2023).

## Set-up
- **Portfolio:** \$1,000,000 split equally across five ETFs: SPY, BND, GLD, QQQ and VTI.
- **Data:** 15 years of daily adjusted close prices from Yahoo Finance (`yfinance`), converted to log returns.
- **Horizon:** 30 trading days. **Confidence levels:** 95% and 99% (the parametric notebook also shows 90%).

## Notebooks
| Notebook | Method |
|---|---|
| `1_historical_var.ipynb` | **Historical simulation:** the empirical percentile of rolling 30-day portfolio returns |
| `2_parametric_var.ipynb` | **Variance-covariance:** annualised covariance matrix, normal quantile, scaled by √(30/252) |
| `3_monte_carlo_var.ipynb` | **Monte Carlo:** 10,000 simulated 30-day gain/loss scenarios from the portfolio's mean and standard deviation |
| `4_var_backtesting.ipynb` | **Backtest check:** 1-day historical VaR at 99% on the latest month of returns (October 2023), to set against the 15-year estimates |

Each notebook plots the distribution of portfolio gains and losses with the VaR threshold marked.

## How to run
```bash
pip install -r requirements.txt
jupyter notebook
```
Newer `yfinance` versions return auto-adjusted prices by default. If `data['Adj Close']` fails, use `yf.download(..., auto_adjust=False)`.

## Author
Taryll Miranda: MSc Quantitative Finance with Data Science (Distinction), CFA Level I.
