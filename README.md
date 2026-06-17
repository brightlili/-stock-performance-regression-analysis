# Stock Performance Regression Analysis
A Python-based financial data analysis project applying multiple linear regression and hypothesis testing to S&amp;P 500 time series data. Includes EDA, stationarity transformation, autocorrelation detection, and statistical visualization using Statsmodels, Pandas, NumPy, and Seaborn.


Quantitative analysis of US equity fund stock performance using the **Fama/French 5 Factor Model** with multiple linear regression and hypothesis testing in Python.

---

## Project Background

The fund management team of a US equity fund sought to adopt a more quantitative (factor investing) approach to improve fund performance. The finance & analytics team was tasked with identifying which macroeconomic and style factors drive individual stock performance and how significantly each factor contributes.

---

## Objectives

- Fit one multiple linear regression model per stock (15 stocks total) using the Fama/French 5 Factors
- Test the statistical significance of all regression coefficients at the **5% significance level**
- Conduct Explanatory Data Analysis (EDA) and statistical data visualization
- Pre-process financial time series data (stationarity transformation)
- Detect and handle autocorrelation (serial correlation) in regression residuals
- Rank the five factors by importance across all stocks
- Produce two results tables for the fund management team

---

## Datasets

| File | Description |
|---|---|
| `stock_prices.csv` | Daily stock prices for 15 US equities (2020–2022) |
| `factors.csv` | Daily Fama/French 5 Factors + Risk-Free Rate (RF) |

### Stocks Covered (15)
`AAPL` `AJG` `AVB` `DLR` `ICE` `INCY` `KHC` `LLY` `MCHP` `MDT` `MOH` `NDAQ` `PRU` `STLD` `TER`

### Fama/French 5 Factors
| Factor | Description |
|---|---|
| `Mkt_Prem` | Market Risk Premium (Rm − Rf) |
| `SMB` | Size: Small Minus Big |
| `HML` | Value: High Minus Low (Book/Market) |
| `RMW` | Profitability: Robust Minus Weak |
| `CMA` | Investment: Conservative Minus Aggressive |
| `RF` | Risk-Free Rate (1-month T-bill) |

---

## Methodology

### 1. Data Pre-processing
- Converted daily stock **prices → returns** using `.pct_change().mul(100)`
- Computed **excess returns** (stock return − RF) to use as the dependent variable
- Merged stock returns and factor data by date

### 2. Exploratory Data Analysis (EDA)
- Visualized raw prices and returns for stationarity check
- Computed pairwise correlation matrix for AAPL (showcase stock)
- Generated seaborn heatmap, pairplot, and lmplot

### 3. Regression Modelling
- Defined and fitted one OLS model per stock using `statsmodels.formula.api`
- Model formula: `Stock_Excess_Return ~ Mkt_Prem + SMB + HML + RMW + CMA`
- Extracted regression coefficients and R-squared for all 15 models

### 4. Hypothesis Testing
- Tested all coefficients (intercept + 5 slopes) at **α = 5%** significance level
- Result: `True` (p-value < 0.05) = significant, `False` = not significant

### 5. Autocorrelation Check
- Visualised regression residuals for AAPL
- Applied **Durbin-Watson test**: DW ∈ [1.6, 2.4] → no autocorrelation

### 6. Factor Importance Ranking
- Calculated the proportion of stocks for which each factor is significant
- Ranked factors from most to least important

---

## Key Findings

- **Mkt_Prem** is the most important factor — significant for 100% of stocks
- The Fama/French 5 Factor Model explains on average **>50% of stock return variation** (mean R²)
- Marginal benefit of additional factors (HML, SMB, CMA, RMW) declines beyond market premium
- No autocorrelation detected in residuals (Durbin-Watson within [1.6, 2.4])

---

## Project Structure

```
stock-performance-regression-analysis/
│
├── data/
│   ├── stock_prices.csv          # Daily stock prices (15 stocks)
│   └── factors.csv               # Fama/French 5 Factors + RF
│
├── notebooks/
│   └── Time_Series_Regression.ipynb   # Full analysis notebook
│
├── outputs/
│   └── final_report.pdf          # Final deliverable for fund management team
│
├── README.md
├── requirements.txt
└── .gitignore
```

---

## Setup & Installation

### 1. Clone the repository
```bash
git clone https://github.com/yourusername/stock-performance-regression-analysis.git
cd stock-performance-regression-analysis
```

### 2. Create and activate virtual environment
```bash
python -m venv venv
source venv/bin/activate        # Mac/Linux/Codespaces
# venv\Scripts\activate         # Windows
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Launch Jupyter
```bash
jupyter notebook
```

Open `notebooks/Time_Series_Regression.ipynb` and select the **Python (venv)** kernel.

---

## Requirements

```
pandas
numpy
matplotlib
seaborn
statsmodels
jupyter
ipykernel
```

See `requirements.txt` for pinned versions.

---

## Results

### Table 1 — Regression Coefficients
15 × 6 table of OLS coefficients (Intercept + 5 factor slopes) per stock.

### Table 2 — Significance & R-squared
15 × 7 table of True/False significance flags per coefficient + R-squared per model.

### Factor Importance Ranking (High → Low)
1. **Mkt_Prem** — Market Risk Premium
2. **SMB** — Size
3. **HML** — Value
4. **RMW** — Profitability
5. **CMA** — Investment

---

## License

MIT License — see `LICENSE` for details.

---

## References

- Fama, E. F., & French, K. R. (2015). *A five-factor asset pricing model*. Journal of Financial Economics.
- [Kenneth French Data Library](https://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html)
- [Statsmodels Documentation](https://www.statsmodels.org/)

