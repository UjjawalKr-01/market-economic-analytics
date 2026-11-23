# Market & Economic Analytics

### Exploring 70 Years of US Macroeconomic Trends, Financial Markets & Time-Series Forecasting

An end-to-end data analytics project investigating historical US economic behaviour through inflation, unemployment, monetary policy, and equity market indicators. Combining exploratory data analysis, statistical correlation analysis, and Prophet-based time-series forecasting to understand historical patterns and evaluate potential future trends.

<p align="center">
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white"/>
  <img src="https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white"/>
  <img src="https://img.shields.io/badge/Scikit--learn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white"/>
  <img src="https://img.shields.io/badge/Prophet-000000?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white"/>
  <img src="https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Seaborn-4C72B0?style=for-the-badge"/>
</p>

<p align="center">
  <a href="https://fred.stlouisfed.org/">
    <img src="https://img.shields.io/badge/Data%20Source-FRED-1B365D?style=for-the-badge"/>
  </a>
</p>

---

## Overview

Economic indicators are interconnected, but their relationships can change significantly across different periods and economic conditions.

This project explores approximately seven decades of US macroeconomic data, examining the historical behaviour of major economic indicators and their relationships with financial markets.

The analysis combines historical economic data with statistical techniques and time-series forecasting to investigate economic trends, identify correlations, and evaluate the practical limitations of predictive modelling.

### Key Objectives

- Analyse long-term US macroeconomic trends from 1954 to 2025.
- Investigate historical inflation and unemployment patterns.
- Examine Federal Funds Rate movements and monetary policy cycles.
- Explore the relationship between macroeconomic indicators and equity markets.
- Apply time-series forecasting to selected economic and financial indicators.
- Evaluate model performance and identify limitations in long-term economic forecasting.

## Key Highlights

- Approximately 70 years of historical US macroeconomic analysis.
- Integration of four major economic and financial indicators.
- Separate datasets for long-term macroeconomic analysis and recent combined analysis.
- Exploratory data analysis and statistical correlation analysis.
- Indicator-specific time-series forecasting using Prophet.
- Forecast evaluation using MAE and RMSE.
- Investigation of forecasting limitations, trend behaviour, and uncertainty.

## Technology Stack

| Technology | Purpose |
|---|---|
| Python | Core programming language |
| Pandas | Data manipulation and preprocessing |
| NumPy | Numerical operations |
| Scikit-learn | Statistical and analytical utilities |
| Prophet | Time-series forecasting |
| Matplotlib | Data visualisation |
| Seaborn | Statistical visualisation |
| Jupyter Notebook | Interactive analysis and experimentation |

## Data Sources

The primary data source for this project is [Federal Reserve Economic Data (FRED)](https://fred.stlouisfed.org/).

Four major indicators were selected for the analysis:

| Indicator | FRED Series ID | Description |
|---|---|---|
| Consumer Price Index | `CPIAUCSL` | Measures changes in consumer price levels |
| Unemployment Rate | `UNRATE` | Represents the percentage of the labour force that is unemployed |
| Federal Funds Rate | `FEDFUNDS` | Represents the effective federal funds interest rate |
| S&P 500 | `SP500` | Tracks the performance of the US equity market |

### Dataset Architecture

The project uses two distinct datasets to account for differences in historical data availability.

| Dataset | Coverage | Purpose |
|---|---|---|
| Long-term macroeconomic dataset | 1954–2025 | Historical analysis of CPI, unemployment, and Federal Funds Rate |
| Combined monthly dataset | 2021–2025 | Comparative analysis incorporating all four indicators |

The S&P 500 has a shorter historical coverage in the selected dataset. Combining all indicators using a common date range would have discarded valuable historical macroeconomic information.

To avoid this, the datasets were maintained separately, preserving long-term historical coverage while enabling recent-period comparative analysis.

---

## Exploratory Data Analysis

The exploratory analysis investigates the historical behaviour of individual indicators and identifies patterns across different economic periods.

### 1. Historical Macroeconomic Trends

The long-term analysis focuses on three major indicators covering the period from 1954 to 2025.

#### Consumer Price Index (CPI)

Examines long-term changes in consumer price levels, highlighting inflationary periods and the evolution of prices across several decades.

<!-- INSERT VISUAL: visuals/cpi_trend_long_history.png -->

#### US Unemployment Rate

Explores historical labour-market conditions and fluctuations in unemployment across different economic periods.

<!-- INSERT VISUAL: visuals/unrate_trend_long_history.png -->

#### Federal Funds Rate

Examines historical monetary policy movements, including major interest-rate cycles and changes in the federal funds rate.

<!-- INSERT VISUAL: visuals/fedfunds_trend_long_history.png -->

### 2. Macroeconomic Correlation Analysis

Correlation analysis was performed to investigate relationships between the selected economic indicators.

#### Long-Term Correlation (1954–2025)

The historical correlation analysis examines relationships between CPI, unemployment, and the Federal Funds Rate.

<!-- INSERT VISUAL: visuals/correlation_heatmap_long_history.png -->

#### Recent Correlation Including S&P 500 (2021–2025)

The combined dataset enables correlation analysis across all four indicators, including the S&P 500.

<!-- INSERT VISUAL: visuals/correlation_heatmap_recent_with_sp500.png -->

The recent-period analysis provides an additional perspective on the relationships between inflation, labour-market conditions, interest rates, and equity market movements.

**Note:** Correlation measures statistical association, not causation. Results are also sensitive to the selected observation period and economic conditions.

### 3. Recent S&P 500 Market Trend

The S&P 500 was analysed separately to examine its recent historical performance.

<!-- INSERT VISUAL: visuals/sp500_trend_recent.png -->

This analysis provides historical context for the subsequent S&P 500 forecasting exercise.

---

## Time-Series Forecasting

Prophet was used to develop forecasting models for selected economic and financial indicators.

Rather than assuming that all economic series follow identical patterns, separate forecasting approaches were considered according to the behaviour of each indicator.

The forecasting exercises cover a five-year horizon, with the resulting estimates and uncertainty intervals visualised alongside historical observations.

### 1. CPI Forecast

The CPI forecasting model explores the continuation of historical price-level trends over the forecast horizon.

<!-- INSERT VISUAL: visuals/cpi_forecast.png -->

### 2. Federal Funds Rate Forecast

The Federal Funds Rate model examines potential future rate movements while accounting for the bounded nature of the selected forecasting approach.

<!-- INSERT VISUAL: visuals/fedfunds_forecast.png -->

### 3. S&P 500 Forecast

The S&P 500 forecasting model investigates potential future equity-index trends using its available historical observations.

<!-- INSERT VISUAL: visuals/sp500_forecast.png -->

The widening uncertainty interval highlights the difficulty of extrapolating financial market behaviour over extended periods.

---

## Model Evaluation

Forecasting performance was evaluated using standard regression error metrics.

| Metric | Description |
|---|---|
| MAE | Mean Absolute Error — measures the average absolute prediction error |
| RMSE | Root Mean Squared Error — penalises larger prediction errors more heavily |

The evaluation process considers the difference between actual and predicted values, rather than relying exclusively on visual inspection of forecast plots.

Actual model scores should be reported alongside the corresponding indicator and evaluation period.

## Model Refinement & Analytical Considerations

During model development, several important forecasting considerations were identified:

- **Trend continuity:** Forecasts should connect appropriately with the historical series without introducing artificial discontinuities.
- **Evaluation methodology:** Training and evaluation periods must be separated appropriately to avoid misleading performance estimates.
- **Bounded forecasting:** Interest-rate indicators require consideration of their bounded behaviour rather than unrestricted extrapolation.
- **Forecast uncertainty:** Wider uncertainty intervals indicate greater uncertainty in future estimates.
- **Economic regime changes:** Historical relationships may not remain stable under changing monetary, financial, and economic conditions.

These considerations are important when interpreting forecasts of economic indicators, where unexpected events and policy decisions can significantly alter historical patterns.

## Limitations

Long-term economic forecasting involves uncertainty that cannot be eliminated through statistical modelling alone.

The main limitations include:

- **Historical dependency:** Forecasting models rely on historical observations and may not anticipate unprecedented economic events.
- **Structural changes:** Economic relationships can change across different monetary and economic regimes.
- **Limited S&P 500 history:** The shorter observation window limits the historical information available for training and evaluation.
- **Monetary policy uncertainty:** Federal Funds Rate movements depend on policy decisions and changing economic conditions.
- **Forecast uncertainty:** Predictions become less certain as the forecast horizon increases.

The generated forecasts should therefore be interpreted as model-based estimates rather than definitive predictions of future economic conditions.

---

## Project Structure

```text
market-economic-analytics/
│
├── visuals/
│   ├── cpi_trend_long_history.png
│   ├── unrate_trend_long_history.png
│   ├── fedfunds_trend_long_history.png
│   ├── correlation_heatmap_long_history.png
│   ├── correlation_heatmap_recent_with_sp500.png
│   ├── sp500_trend_recent.png
│   ├── indexed_indicators_2021_2025.png
│   ├── cpi_forecast.png
│   ├── fedfunds_forecast.png
│   └── sp500_forecast.png
│
├── notebooks/
│   └── Jupyter analysis notebooks
│
├── data/
│   └── Raw and processed datasets
│
├── reports/
│   └── Analytical and model evaluation reports
│
├── requirements.txt
└── README.md
```

*The directory layout above describes the intended organisation; adjust folder names to match the actual repository.*

## Installation & Execution

### 1. Clone the Repository

```bash
git clone https://github.com/UjjawalKr-01/market-economic-analytics.git

cd market-economic-analytics
```

### 2. Create a Virtual Environment

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Launch Jupyter Notebook

```bash
jupyter notebook
```

Open the project's notebooks and execute the data preparation, exploratory analysis, and forecasting stages in their intended order.

*The commands assume the repository contains a compatible `requirements.txt` and Jupyter notebooks.*

---

## Skills Demonstrated

- Data Collection and Preprocessing
- Exploratory Data Analysis (EDA)
- Statistical Analysis and Correlation
- Macroeconomic Data Analysis
- Time-Series Analysis
- Predictive Modelling
- Forecast Evaluation
- Data Visualisation
- Analytical Problem Solving
- Working with Real-World Economic Datasets

## Future Improvements

Potential directions for extending the project include:

- Expanding the analysis to additional international economic indicators.
- Incorporating more financial and macroeconomic datasets.
- Comparing Prophet with alternative time-series forecasting techniques.
- Introducing rolling-window and walk-forward validation.
- Investigating economic relationships across different historical regimes.
- Developing an interactive dashboard for exploring economic indicators and forecasts.

---

## Author

**Ujjawal Kumar**

GitHub: [UjjawalKr-01](https://github.com/UjjawalKr-01)

Repository: [Market & Economic Analytics](https://github.com/UjjawalKr-01/market-economic-analytics)

---

*An independent data analytics project exploring historical macroeconomic behaviour, financial market trends, and the practical challenges of time-series forecasting.*
