# Vendor Sales & Profitability Analysis

![Python](https://img.shields.io/badge/Python-3.x-blue)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-orange)
![SQL Server](https://img.shields.io/badge/SQL-Server-green)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

---

## Project Overview

An end-to-end data analysis pipeline built on a beverage distribution company's procurement and sales data. Raw CSV files are ingested into a local SQL Server database via SQLAlchemy, a consolidated reporting table is engineered using multi-table SQL CTEs, and all business analysis is performed on top of that table using Python.

The goal is to help procurement teams identify high-performing vendors, flag inventory risks, and optimize purchasing decisions.

---

## Tech Stack

| Tool | Usage |
|------|-------|
| Python 3.x | Data pipeline & analysis |
| Pandas & NumPy | Data cleaning, feature engineering |
| SQLAlchemy + pyodbc | Python ↔ SQL Server integration |
| SQL Server | Data storage, CTEs, aggregations |
| Matplotlib & Seaborn | Visualizations |
| SciPy | Statistical hypothesis testing |

---

## Project Structure

```
vendor-procurement-analytics/
├── data/                          # Raw CSV input files (not committed)
├── vendor_analysis.ipynb          # Main analysis notebook
└── README.md
```

---

## Pipeline Walkthrough

### Step 1 — Data Ingestion
CSV files are loaded from the `data/` folder and pushed to SQL Server tables using `pandas.to_sql()` via SQLAlchemy.

### Step 2 — SQL Feature Engineering
A consolidated `vendor_sales_summary` table is built using a 3-layer CTE query joining:
- `purchases` — transaction-level purchase records
- `purchase_prices` — actual product pricing
- `sales` — revenue and quantity sold
- `vendor_invoice` — freight costs per vendor

Data quality fix applied at this stage: records with `PurchasePrice = 0` were excluded (data entry errors confirmed on inspection).

### Step 3 — Data Cleaning (Python)
- `inf` / `-inf` values replaced using `numpy` (caused by division in ratio columns)
- NaN values from LEFT JOIN mismatches filled with 0 (vendor purchased but no sales record)
- `VendorName` whitespace stripped using `.str.strip()`
- Column types enforced before SQL write (`DECIMAL(10,3)`, `INT`)
- Primary key added on `(VendorNumber, Brand)`

### Step 4 — Derived Metrics
```python
GrossProfit         = TotalSalesDollars - TotalPurchaseDollars
ProfitMargin        = (GrossProfit / TotalSalesDollars) * 100
StockTurnover       = TotalSalesQuantity / TotalPurchaseDollars
SalestoPurchaseRatio = TotalSalesDollars / TotalPurchaseDollars
UnitPurchasePrice   = TotalPurchaseDollars / TotalPurchaseQuantity
UnsoldInventoryValue = (TotalPurchaseQuantity - TotalSalesQuantity) * PurchasePrice
```

### Step 5 — EDA & Cleaning
- Distribution plots for all numeric columns
- Outlier detection via box plots
- Correlation heatmap across all metrics
- Removed rows with negative GrossProfit, negative ProfitMargin, or zero TotalSalesQuantity for cleaner downstream analysis

---

## Research Questions Answered

| # | Question |
|---|----------|
| 1 | Which brands have low sales but high profit margins? (promotion candidates) |
| 2 | Which vendors and brands drive the highest total sales? |
| 3 | Which vendors contribute the most to total purchase spend? |
| 4 | How concentrated is procurement among the top 10 vendors? |
| 5 | Does bulk purchasing reduce unit price? What is the cost difference by order size? |
| 6 | Which vendors have low inventory turnover (slow-moving stock)? |
| 7 | How much capital is locked in unsold inventory per vendor? |
| 8 | Is the profit margin difference between top and low-performing vendors statistically significant? |

---

## Key Findings

- **Top 2 vendors (Martignetti Companies + Ultra Beverage) account for ~28% of total purchase spend** — high supplier concentration risk
- **Bulk purchasing delivers ~72% reduction in unit price** for large-order vendors vs. small-order vendors (validated via `pd.qcut` segmentation + box plot)
- **Brands in the bottom 15% of sales but top 85% of profit margin** were flagged as promotional candidates and exported to CSV
- **Two-sample T-test result (p < 0.05):** Statistically significant difference in profit margins between top-quartile and bottom-quartile vendors — confirms performance gap is real, not random variation
- **95% Confidence Intervals** calculated separately for top and low-performing vendor groups

---

## Visualizations

- Top 10 vendors and brands by total sales (horizontal bar charts)
- Pareto chart — vendor contribution to total purchase spend with 80% threshold line
- Donut chart — top 10 vs. remaining vendor procurement share
- Scatter plot — brands by sales volume vs. profit margin (with promotion candidates highlighted)
- Box plot — unit price distribution by order size (Small / Medium / Large)
- Distribution histograms and box plots for all numeric columns
- Correlation heatmap
- Confidence interval comparison — top vs. low vendor profit margins

---

## Setup

1. Install dependencies:
   ```bash
   pip install pandas sqlalchemy pyodbc matplotlib seaborn scipy numpy
   ```
2. Install **ODBC Driver 17 for SQL Server** on your machine
3. Place raw CSV files in the `data/` folder
4. Update the SQL Server connection string in Cell 4 with your local server name:
   ```python
   server = r'YOUR_SERVER\SQLEXPRESS'
   database = 'inventory'
   ```
5. Run all cells in order

---

## Author

**Hemant Yadav**
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://www.linkedin.com/in/hemant-yadav-273a60376)
