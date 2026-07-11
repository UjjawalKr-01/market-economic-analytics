# Market & Economic Analytics

A macroeconomic analysis and forecasting project using U.S. inflation,
unemployment, interest-rate, and stock-market data from
[FRED](https://fred.stlouisfed.org/) (Federal Reserve Economic Data).

Data cleaning and merging → exploratory analysis → time-series forecasting
with [Prophet](https://facebook.github.io/prophet/) → Power BI dashboards.

## What's in here

```
Data/raw/            Original FRED CSV exports (CPI, unemployment, Fed Funds, S&P 500)
Data/processed/       Cleaned/merged datasets + forecast outputs
notebook/              01 data loading & cleaning · 02 EDA · 03 predictive modelling
models/                Saved Prophet models (.pkl)
reports/                Accuracy report + correlation tables
visuals/                Exported charts (PNG)
```

## Data

| Series | What it is | History available |
|---|---|---|
| `CPIAUCSL` | Consumer Price Index (inflation) | 1947 – present |
| `UNRATE` | Unemployment rate | 1948 – present |
| `FEDFUNDS` | Federal Funds effective rate | 1954 – present |
| `SP500` | S&P 500 index level (daily) | **~2021 – present only** |

**Important:** FRED's `SP500` series is licensed from S&P and only keeps a
rolling ~5-year window — it's not possible to pull a longer history from this
source. Because of that, this project builds **two** datasets rather than one:

- `macro_long_history.csv` — CPI, unemployment, Fed Funds, back to **1954**
  (857 months)
- `master_monthly_dataset.csv` — all four series together, necessarily limited
  to **2021–2025** (58 months)

Trend analysis and the CPI/Fed Funds forecasts use the long-history dataset.
Anything involving SP500 is working with a much shorter window — flagged
throughout.

## Key findings

- **CPI and the Fed Funds rate move together over the long run** (1954–2025)
  — consistent with the Fed raising rates to fight inflation, which is
  exactly what played out in 2022–2023.
- **Unemployment is negatively correlated with Fed Funds** over the long run,
  broadly consistent with tighter policy cooling the labor market.
- In the 2021–2025 window specifically, **SP500 shows a strong positive
  correlation with CPI and Fed Funds** — but this is a short, single-cycle
  correlation (the post-COVID recovery and AI-driven rally happened to
  coincide with the hiking cycle). It shouldn't be read as a stable
  structural relationship given how little history supports it.
- See `visuals/indexed_indicators_2021_2025.png` for all four series compared
  on a common indexed scale, and `reports/correlation_long_history.csv` /
  `correlation_recent_with_sp500.csv` for the full numbers.

## Forecasting methodology

Prophet models were trained per series and evaluated on a holdout matched to
the forecast horizon (~5 years), not an arbitrary 80/20 split — a naive
80/20 split on 70 years of data tests 14-years-ahead accuracy, which
understates real near-term error.

| Series | Approach | Why |
|---|---|---|
| CPI | Linear trend on **log(CPI)**, trained on full 1954–2025 history | A price index grows roughly exponentially; modeling it directly with a linear trend underfits recent acceleration |
| Fed Funds | **Logistic (bounded) growth**, capped 0–12%, full history | A policy rate is mean-reverting and cyclical, not a growth trend — bounding it prevents runaway extrapolation |
| S&P 500 | Linear trend on log(SP500), trained on the only available window (2021–2025) | Best available given the data limitation above |

**Accuracy (see `reports/model_accuracy.txt` for the live-generated version):**

| Series | MAE | RMSE | Notes |
|---|---|---|---|
| CPI | ~25 | ~27 | Holdout period includes the 2021–23 inflation shock — a genuine structural break no pre-2021-trained model could anticipate |
| Fed Funds | ~3.0 | ~3.5 | Holdout includes the 2022–23 hiking cycle from near-zero |
| S&P 500 | ~189 | ~273 | Only 58 months of training data available |

These numbers are **higher** than what you'd get from an easier evaluation
window — that's intentional. It's a more honest measurement, not a worse
model.

## Limitations (read before trusting the forecasts)

- **S&P 500 forecast is low-confidence.** With only ~5 years of training
  data, uncertainty compounds hugely over a 5-year horizon. Treat the point
  forecast as directional at best; the raw confidence interval (in the CSV)
  is close to meaningless beyond ~12–18 months out. The chart in `visuals/`
  caps the shaded band at 2x for readability — the full uncertainty is in
  `Data/processed/sp500_forecast_2025_2030.csv`.
- **Fed Funds is a fundamentally hard series to trend-extrapolate.** It's
  policy-driven and cyclical, not a growing quantity. An earlier version of
  this project's model extrapolated a straight line from the 2022–23 hiking
  cycle and forecast the rate climbing to 8%+ by 2026 — while the actual rate
  was falling. That's fixed here (bounded growth + a boundary-continuity
  correction so the forecast starts exactly at the last real observation),
  but a 5-year Fed Funds forecast from trend extrapolation alone should still
  be read as "roughly flat to gently declining, wide uncertainty," not a
  precise number.
- **CPI's forecast is the most defensible** of the three — 70 years of
  training data and inflation does have real multi-year persistence — but it
  still assumes no future shock on the scale of 2021–23, which is by
  definition unknowable in advance.

## Reproducing this

```bash
pip install -r requirements.txt
```

Run the notebooks in order: `01_data_loading_cleaning.ipynb` →
`02_eda.ipynb` → `03_predictive_modelling.ipynb`. Each writes its outputs to
`Data/processed/`, `visuals/`, `models/`, and `reports/`, so later notebooks
depend on earlier ones having been run first.
