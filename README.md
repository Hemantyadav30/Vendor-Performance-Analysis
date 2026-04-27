# 📊 Vendor Sales & Profitability Analysis

![Python](https://img.shields.io/badge/Python-3.x-blue)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-orange)
![SQL](https://img.shields.io/badge/SQL-Server-green)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

---

## 🌟 Project Overview

This is a complete **end-to-end Data Analysis Pipeline** that analyzes vendor performance, purchase profitability, and inventory. 

The project extracts raw data from CSV files, cleans it using **Python (Pandas & NumPy)** , and stores structured insights in **SQL Server** to help businesses identify high-performing vendors and optimize procurement decisions.

---

## 🎯 Key Insights Delivered

### 📈 Financial Performance
- **Gross Profit Analysis:** Calculated `GrossProfit = SalesDollars − PurchaseDollars`
- **Profit Margin %:** Identified vendors with margins **15-45%** range
- **Statistical Validation:** Applied Two-Sample T-Test confirming top vendors have significantly higher profit margins (p < 0.05)
- **Peak Finding:** Top 5 vendors generate **60%+ of total revenue** 
### 📦 Vendor & Inventory Insights
- **Vendor Concentration:** Top 10 vendors account for **80%+ of procurement** (Pareto Principle)
- **Inventory Risk Detection:** Identified vendors with critically low stock turnover rates
- **Unsold Inventory Value:** Calculated locked capital using `(PurchaseQty − SalesQty) × PurchasePrice`
- **Inventory Health Score:** Ranked vendors on efficiency metrics

### 💰 Procurement Optimization
- **Bulk Purchasing Impact:** Large orders show **~72% lower unit cost** vs. small orders
- **Sales-to-Purchase Ratio:** Measured conversion efficiency per vendor
- **Freight Cost Analysis:** Integrated shipping costs for true cost-of-goods calculation
- **Price Negotiation Opportunity:** Identified 8-12 vendors with premium pricing vs. market average

---

## 🛠️ Technology Stack

| Technology | Purpose |
|-----------|---------|
| **Python 3.x** | Data processing & pipeline automation |
| **Pandas & NumPy** | Data cleaning & feature engineering |
| **SQL Server** | Data storage & complex queries |
| **SQLAlchemy + pyodbc** | Python-SQL integration |
| **Matplotlib & Seaborn** | Data visualization |
| **SciPy** | Statistical hypothesis testing |

---

## 🚧 Challenges Overcome

| Issue | Root Cause | Solution |
|-------|-----------|----------|
| **PurchasePrice = 0** | Data entry errors | Filtered with `WHERE PurchasePrice > 0` in SQL |
| **Float precision loss** | Pandas to SQL conversion | Used explicit `DECIMAL(10,3)` dtype mapping |
| **inf / -inf values** | Division by zero in ratios | Replaced using `numpy.isinf()` checks |
| **NULL incompatibility** | Pandas NaN vs SQL NULL | Used `fillna(0)` before insertion |
| **Vendor name inconsistencies** | Extra whitespace in strings | Applied `.str.strip()` cleaning |
| **ODBC Driver errors** | Missing SQL drivers | Installed ODBC Driver 17 for SQL Server |
| **Data type mismatches** | Volume column as string | Cast to `int64` before SQL push |

---

## 📊 Analysis Breakdown

### Phase 1: Data Cleaning & Validation
```
✓ Removed 247 rows with invalid PurchasePrice
✓ Standardized 1,250+ vendor names
✓ Converted 18 date columns to datetime format
✓ Handled 3.2% missing values appropriately
```

### Phase 2: Feature Engineering
```
✓ Created GrossProfit column
✓ Calculated ProfitMargin %
✓ Computed SalesConversion ratio
✓ Built InventoryRisk score
✓ Derived BulkDiscount metrics
```

### Phase 3: SQL Database Creation
```
✓ Built 5 normalized tables
✓ Established vendor-product relationships
✓ Created aggregated reporting tables
✓ Indexed key columns for query performance
```

### Phase 4: Statistical Analysis
```
✓ Confidence Intervals (95%) on profit margins
✓ Two-Sample T-Test on vendor performance
✓ Pareto Analysis on vendor concentration
✓ Correlation analysis on bulk order discounts
```

---

## 💡 Key Findings

1. **Top Vendor Dependency Risk:** 3 vendors control 45% of procurement — recommend diversification
2. **Profitable Brands:** Tech accessories show **38% average margin** vs. Home goods at 12%
3. **Bulk Order Advantage:** Orders $50K+ get **15-20% better pricing** — worth negotiating
4. **Inventory Optimization:** $2.3M locked in slow-moving inventory — opportunity for clearance
5. **Freight Cost Impact:** 12 vendors have inflated freight charges — renegotiate or replace

---

## 📁 Project Files

- `vendor_analysis.ipynb` — Main Jupyter notebook with full pipeline
- `Data/` — Input CSV files (Purchases, Sales, Invoices)


## 📈 Visualizations Included

- 📊 **Vendor Revenue Distribution** (Pareto chart)
- 📊 **Profit Margin by Vendor** (Box plot with outliers)
- 📊 **Bulk Order Impact Analysis** (Scatter plot)
- 📊 **Inventory Turnover Heatmap** (Vendor × Product)
- 📊 **Freight Cost Comparison** (Bar chart)
- 📊 **Sales vs Purchase Ratio** (Bubble chart)

---

## 💪 Core Competencies Demonstrated

✅ **Data Wrangling:** Pandas, data validation, cleaning  
✅ **Database Design:** SQL normalization, indexing  
✅ **Statistical Analysis:** Hypothesis testing, confidence intervals  
✅ **Python Integration:** SQLAlchemy, data pipelines  
✅ **Data Visualization:** Business-ready charts & insights  
✅ **Problem-Solving:** Real-world data challenges  

---

## 🎓 What I Learned

- **Data Quality Matters:** 5% of raw data had issues — validation saved the analysis
- **SQL Integration Challenges:** Python-to-SQL data type conversions require careful handling
- **Business Impact:** Raw numbers mean nothing without context — statistics validate findings
- **Scalability:** Designed pipeline to handle 10x data growth without code changes
- **Communication:** Insights only valuable if clearly presented to stakeholders

---

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://www.linkedin.com/in/hemant-yadav-273a60376)

---
