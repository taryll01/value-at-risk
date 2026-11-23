# Value at Risk and Expected Shortfall: Historical, Parametric and Monte Carlo

Compares three ways of measuring the **Value at Risk (VaR)** and **Expected Shortfall (ES)** of a portfolio, then backtests all three out of sample on October 2023.

## Set-up
- **Portfolio:** \$1,000,000 split equally across five ETFs: SPY, BND, GLD, QQQ and VTI.
- **Data:** 15 years of daily adjusted close prices to 30 September 2023 from Yahoo Finance (`yfinance`), converted to log returns.
- **Horizon:** 30 trading days. **Confidence levels:** 95% and 99% (the parametric notebook also shows 90%).

## Notebooks
| Notebook | Method |
|---|---|
| `1_historical_var.ipynb` | **Historical simulation:** VaR is the empirical percentile of rolling 30-day returns; ES is the average return beyond it |
| `2_parametric_var.ipynb` | **Variance-covariance:** normal VaR and closed-form normal ES from the covariance matrix, scaled by √(30/252) |
| `3_monte_carlo_var.ipynb` | **Monte Carlo:** 10,000 simulated 30-day gain/loss scenarios; VaR and ES from the simulated tail |
| `4_var_backtesting.ipynb` | **Out-of-sample backtest:** 1-day VaR and ES from all three methods, tested on every trading day of October 2023 (exceedances, and actual vs forecast tail loss) |

## Results
**30-day horizon, \$1m portfolio**

| Method | VaR 95% | ES 95% | VaR 99% | ES 99% |
|---|---|---|---|---|
| Historical | \$46,513 | \$81,007 | \$108,588 | \$146,774 |
| Parametric | \$74,827 | \$93,836 | \$105,829 | \$121,244 |
| Monte Carlo | \$64,486 | \$83,616 | \$94,769 | \$111,887 |

**Backtest, October 2023 (22 trading days, 1-day horizon)**
- **No breaches:** none of the methods was breached at 95% or 99%. The worst day (25 Oct) lost \$11,517, just under the tightest 95% VaR (Historical, \$12,216).
- **Tail risk:** at 99%, Historical ES is \$34,787, while the normal-based Parametric (\$21,776) and Monte Carlo (\$21,820) ES are about **37% lower**. The normal distribution understates fat-tailed losses, which ES picks up and VaR alone hides.
- **Small sample:** one month is a sense check, not a formal backtest such as Kupiec's test.

## How to run
```bash
pip install -r requirements.txt
jupyter notebook
```

## History
The VaR notebooks were written in October–November 2023. Expected Shortfall, the fixed end dates and random seed (for reproducible results), and the out-of-sample backtest of all three methods were added in November 2026.

## Author
Taryll Miranda: MSc Quantitative Finance with Data Science (Distinction), CFA Level I.
