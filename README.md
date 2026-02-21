# Financial Statement Analysis of LG Energy Solution

A project analyzing LG Energy Solution's financial statements and estimating firm value using modern valuation models (RIM & EVA).

## 📁 Project Structure

```
Financial-statement-analysis-of-LG-energy-solution/
├── 01_financial_statements/
│   ├── financial_statements.xlsx           # Raw financial statement data
│   ├── financial_statements_revised.xlsx   # Cleaned & revised version
│   └── extract_financial_data.py           # DART API data extraction script
├── 02_ratio_analysis/
│   ├── ratio_analysis_revised.xlsx         # Computed financial ratios
│   ├── ratio_analysis_solutions.pdf        # Ratio analysis problem solutions
│   └── ratio_analysis.py                   # Ratio calculation script
├── 03_estimated_statements/
│   ├── estimated_financial_statements.xlsx # Projected income statement & balance sheet
│   └── build_estimated_statements.py       # Script to build projected statements
└── 04_valuation/
    └── rim_eva_valuation.py                # RIM & EVA firm valuation models
```

## 📌 Analysis Pipeline

1. **Financial Data Extraction** — Retrieve consolidated financial reports from DART using `dart_fss`
2. **Ratio Analysis** — Compute profitability, liquidity, leverage, and efficiency ratios
3. **Estimated Financial Statements** — Project future income statements and balance sheets
4. **RIM Valuation** — Estimate present equity value using the Ohlson Residual Income Model
5. **EVA Valuation** — Estimate present equity value using the Economic Value Added model

## 🛠 Tech Stack

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white)
![Excel](https://img.shields.io/badge/Excel-217346?style=flat&logo=microsoft-excel&logoColor=white)

## 📦 Libraries

| Library | Usage |
|---|---|
| `dart_fss` | Fetch financial disclosures from DART (Korea's public filing system) |
| `OpenDartReader` | Alternative DART API reader |
| `pandas` | Data manipulation and Excel I/O |
| `numpy` | Numerical computation |
