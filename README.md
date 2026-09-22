# Real-World Retail Data Cleaning and Exploratory Analysis

## Project Overview

This project is part of the **IBM SkillsBuild Data Analytics with AI Academic Internship Program 2026** (BharatCares / AICTE). It demonstrates a complete, production-grade data analytics workflow applied to a real-world retail dataset — from raw, uncleaned CSV data through systematic cleaning, exploratory data analysis, and business insight generation. All work is performed programmatically in Python using Pandas, NumPy, Matplotlib, and Seaborn.

---

## Problem Statement

A retail business collects order records across multiple international markets (France, Morocco, UK, Spain, Germany, and others). The raw data contains missing values, duplicate order IDs, inconsistent brand and country formatting, free-text weight fields, and records in multiple languages. Without systematic cleaning, any reporting or analytics built on this data will produce inaccurate results — wrong revenue figures, inflated/deflated product rankings, and misleading market insights. The goal is to clean the data programmatically, validate the cleaned output, and derive actionable business insights.

---

## Objectives

1. Perform a rigorous data quality assessment on the raw dataset.
2. Clean the dataset programmatically without modifying the original CSV.
3. Standardize column names, text fields, brand names, and country values.
4. Handle missing values using statistically justified methods.
5. Parse dates and extract order_year, order_month, order_quarter, order_dayofweek.
6. Extract a numeric weight (grams) from the free-text `Raw_Weight` field.
7. Produce a validated, analysis-ready cleaned DataFrame.
8. Perform exploratory data analysis with professional visualizations.
9. Derive actionable business insights from the cleaned data.

---

## Dataset

| Attribute | Detail |
|-----------|--------|
| **Dataset name** | online_retail_real_world.csv |
| **Dataset source** | https://www.kaggle.com/datasets/nudratabbas/real-world-retail-data-for-data-cleaning-easy |
| **Rows** | 3,000 |
| **Columns** | 8 |

### Column Descriptions

| Column | Description |
|--------|-------------|
| `OrderID` | Unique order identifier (format REC-XXXXXX) |
| `CustomerID` | Numeric customer identifier |
| `ProductName` | Name of the product ordered |
| `Brand` | Brand name(s) of the product |
| `Raw_Weight` | Product weight as free-text (e.g. '100 g', '500 ml') |
| `Country` | Comma-separated list of countries where the product is sold |
| `OrderDate` | Date the order was placed (YYYY-MM-DD string) |
| `UnitPrice` | Price per unit (float) |

---

## Data Cleaning Performed

The following data quality issues were identified and resolved:

| Issue | Scope | Resolution |
|-------|-------|-----------|
| Missing `ProductName` | 96 rows (3.2%) | Filled with `'Unknown Product'` placeholder |
| Missing `Brand` | 335 rows (11.2%) | Standardised case + filled with `'Unknown Brand'` |
| Missing `UnitPrice` | 385 rows (12.8%) | Imputed with dataset median (13.16); flagged via `price_imputed` column |
| Missing `Raw_Weight` | 512 rows (17.1%) | Numeric weight extracted where possible; unextractable → NaN |
| Duplicate `OrderID` values | 8 pairs (16 rows) | Each duplicate ID disambiguated by appending `_1` / `_2` suffix |
| Brand capitalisation variants | 120 groups | Unified to Title Case (e.g. 'LU', 'lu', 'Lu' → 'Lu') |
| `OrderDate` stored as string | All rows | Parsed to `datetime64`; year/month/quarter/day features extracted |
| `Raw_Weight` free-text field | 2,488 non-null rows | Regex extraction of first numeric value + unit conversion to grams |
| `Country` multi-valued / tagged | All rows | First country extracted; `en:` prefixes removed; codes mapped to English names |
| Fully empty records | 10 rows | Dropped (no product, brand, weight, or price) |

---

## Exploratory Data Analysis

The EDA performed on the cleaned dataset includes:

- **UnitPrice distribution** — histogram and boxplot showing a near-uniform price spread between 1 and 25
- **Brand frequency analysis** — top 15 brands by order count
- **Country market analysis** — top 15 primary countries by order volume
- **Time series analysis** — orders by year, month, quarter, and day of week
- **Weight distribution** — histogram and boxplot of product weights in grams
- **Price by brand** — average unit price for brands with ≥10 orders
- **Price by country** — boxplot of price distribution across top 5 markets
- **Price tier segmentation** — orders grouped into Budget/Mid-range/Premium/Luxury tiers
- **Product frequency ranking** — top 20 most-ordered products
- **Correlation heatmap** — pairwise correlations between numeric features

---

## Visualizations

The following charts are generated inline in the notebook:

1. `missing_before.png` — Missing values by column before cleaning
2. `missing_after.png` — Before vs After missing value comparison
3. `unitprice_dist.png` — UnitPrice histogram and boxplot
4. `top_brands.png` — Top 15 brands by order count
5. `top_countries.png` — Top 15 primary countries by order count
6. `orders_time.png` — Orders by year and by month
7. `orders_dow.png` — Orders by day of week
8. `weight_dist.png` — Weight distribution (≤1000 g histogram + full boxplot)
9. `avg_price_brand.png` — Average unit price by top brands
10. `orders_quarterly.png` — Order volume by quarter
11. `price_by_country.png` — UnitPrice distribution by top 5 countries
12. `correlation_heatmap.png` — Correlation matrix of numeric features
13. `top_products.png` — Top 20 products by order frequency
14. `price_imputed.png` — Observed vs imputed price counts
15. `price_tier.png` — Orders by price tier

---

## Key Findings

All findings are derived directly from the cleaned dataset:

1. **Dataset** — 2,990 valid orders after removing 10 fully-empty records
2. **Top brand** — Gerblé (57 orders), followed by Hacendado, Carrefour, and Lindt
3. **Dominant market** — France (1,588 orders out of 2,990 ≈ 53%)
4. **Secondary market** — Morocco, ranking second in primary country orders
5. **Price range** — 1.00 to 24.99 (median: 13.16); near-uniform distribution
6. **Median product weight** — 150 g, consistent with snack/biscuit packaging
7. **Missing data root cause** — 17.1% missing weights suggest incomplete product catalog data at order time
8. **Duplicate OrderIDs** — 8 pairs identified, each involving different customers and products (system-level ID generation issue)
9. **120 brand capitalisation conflicts** — resolved through Title Case standardisation
10. **Price is independent of weight** — correlation coefficient near 0

---

## Technologies Used

- **Python** 3.x
- **Pandas** — data manipulation and cleaning
- **NumPy** — numeric operations and NaN handling
- **Matplotlib** — chart generation
- **Seaborn** — statistical visualizations
- **Jupyter Notebook** — interactive analysis environment
- **re (regex)** — free-text weight field parsing

---

## Project Structure

```
Kunnal_RealWorldRetailDataCleaning.ipynb        ← Main Jupyter Notebook
requirements.txt                                 ← Python dependencies
Kunnal_RealWorldRetailDataCleaning_ProjectReport.docx  ← Full project report
README.md                                        ← This file
online_retail_real_world.csv                     ← Raw dataset (unchanged)
```

---

## How to Run

### 1. Install Dependencies

```bash
pip install -r requirements.txt
```

### 2. Ensure the Dataset is Present

The raw CSV file `online_retail_real_world.csv` must be in the same directory as the notebook.

### 3. Launch Jupyter Notebook

```bash
jupyter notebook Kunnal_RealWorldRetailDataCleaning.ipynb
```

### 4. Run All Cells

In Jupyter, select **Kernel → Restart & Run All** to execute the complete notebook from top to bottom. All charts will display inline and be saved as `.png` files in the working directory.

### Alternative: Execute via Command Line

```bash
jupyter nbconvert --to notebook --execute Kunnal_RealWorldRetailDataCleaning.ipynb --output Kunnal_RealWorldRetailDataCleaning.ipynb
```

---

## Conclusion

This project demonstrates that real-world retail data requires significant cleaning before it can be trusted for analysis. The raw dataset contained missing values in four key columns, duplicate order IDs, free-text weight fields, and multi-language country names. A systematic, programmatic cleaning pipeline resolved these issues transparently — preserving all valid data, flagging imputed values, and producing a validated, analysis-ready dataset. The EDA revealed that France is the dominant market, Gerblé leads in order volume, and prices are distributed broadly across all tiers — indicating a retailer serving diverse customer segments across multiple international markets.

---

*IBM SkillsBuild Data Analytics with AI Academic Internship Program 2026 | BharatCares / AICTE | Student: Kunnal*
