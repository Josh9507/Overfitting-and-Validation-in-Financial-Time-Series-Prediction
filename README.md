# Next-Day NVDA Return Forecasting: Lagged Returns and Ridge Regression (revised)

Does a small set of lagged daily returns help predict the next day's NVDA return, compared with a
historical-mean forecast and a zero-return forecast? Development period 2021-2024 (expanding-window
validation), held-out test year 2025.

## Files

| File | Purpose |
|---|---|
| `NVDA_Ridge_Forecasting_Revised.ipynb` | The full analysis; run top to bottom |
| `NVDA_Ridge_Forecasting_Revised.html` | Exported, executed copy of the notebook (outputs and figures embedded) |
| `data/NVDA_raw_2021-2025.csv` | Cached Yahoo Finance download, so results are reproducible |
| `requirements.txt` | Python dependencies |
| `table_*.csv` | Result tables written by the notebook |

## Reproduce

```bash
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook NVDA_Ridge_Forecasting_Revised.ipynb   # Kernel -> Restart & Run All
```

* If `data/NVDA_raw_2021-2025.csv` is present the notebook reads it and needs no internet.
  If it is absent, the notebook downloads the data with `yfinance` and creates it.
* Random seeds are fixed, so bootstrap output is identical on every run.
* Package versions used are printed in the first code cell.

## Contents of the notebook

1. Data and preprocessing
2. Development / test split
3. Expanding-window validation design (fold dates and sizes, aggregation rule)
4. Extended regularization grid (10^-6 to 10^8), validation error vs alpha
5. Overfitting evidence from the folds
6. Historical-mean and zero-return benchmarks
7. Ridge coefficients and stability across folds
8. Block bootstrap on paired forecast-loss differentials

## Limitations

One asset, one test year and five lags; results do not generalize. Lower forecast error is not evidence
of a profitable strategy (no transaction costs, risk or position sizing).
