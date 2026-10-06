# Retail Store Sales Analysis

An end-to-end data analysis project built in **Google Sheets**: data quality checks, cleaning, exploration, analysis, a pivot table, charts and an interactive dashboard, on a retail sales dataset.

**Full workbook (data, cleaning and charts):** (PASTEhttps://docs.google.com/spreadsheets/d/1f6bezGMmQe2t6wFxsFf4QD1H8LLLoKWk-7c8M-ZdY3s/edit?usp=sharing-YOUR-GOOGLE-SHEET-LINK-HERE)

## Project Overview

| Item | Detail |
|---|---|
| Dataset | 12,575 transactions, 11 columns |
| Period | 1 Jan 2022 to 18 Jan 2025 |
| Customers | 25 |
| Product categories | 8 |
| Tool | Google Sheets |

**Goal:** understand how the store sells, which areas perform best, and whether discounts affect sales.

## Files in This Repository

| File | What it is |
|---|---|
| `retail_store_sales.csv` | Original data (raw, with missing values) |
| `retail_store_sales_cleaned.csv` | Cleaned data |
| `retail_sales_dashboard.html` | Interactive dashboard (open in a browser) |
| `README.md` | This report |

## 1. Data Quality Check

| Check | Result |
|---|---|
| Duplicates | None. All 12,575 Transaction IDs are unique |
| Data types | Quantity and Discount Applied needed attention |
| Missing values | Item 1,213, Price Per Unit 609, Quantity 604, Total Spent 604, Discount Applied 4,199 |
| Consistency | Price Per Unit x Quantity = Total Spent in all 11,362 complete rows |
| Validity | No zero, negative or impossible values, no spelling variations, no future dates |
| Outliers | 60 high Total Spent values (404 to 410), all genuine purchases, kept |

## 2. Data Cleaning

| Column | Problem | Fix | Result |
|---|---|---|---|
| Price Per Unit | 609 blanks | Total Spent / Quantity | 0 blanks |
| Item | 1,213 blanks | Looked up from Category + Price (each pair matches exactly one item) | 0 blanks |
| Quantity and Total Spent | 604 blanks in the same rows | Flagged as `Unknown`, not estimated | Kept, excluded from sales totals |
| Discount Applied | 4,199 blanks | Labelled `Unknown` | Kept as its own group |

No rows were deleted and no sales figures were invented.

**Formulas used**

```
Price recovered:        =ARRAYFORMULA(IF(E2:E12576="", G2:G12576/F2:F12576, E2:E12576))
Unknown sales flagged:  =ARRAYFORMULA(IF(F2:F12576="","Unknown","Complete"))
Discount labelled:      =ARRAYFORMULA(IF(K2:K12576="","Unknown",IF(K2:K12576=TRUE,"True","False")))
```

## 3. Exploration: Key Results

- **Total revenue:** 1,552,071 from 11,971 complete sales
- **Average sale:** 129.65
- **Items sold:** 66,276

| Split | Result |
|---|---|
| Top category | Butchers, 208,118 (13.4%) |
| Lowest category | Milk Products, 180,112 (11.6%) |
| Online vs in-store | 51.0% vs 49.0% |
| Payment methods | Cash 34.6%, Credit Card 32.7%, Digital Wallet 32.7% |

## 4. Analysis and Business Insights

1. **Sales are evenly spread** across categories, locations and payment methods. No single area dominates.
2. **Revenue dipped 3.7% in 2023, then grew 6.8% in 2024** (2022: 510,330, 2023: 491,312, 2024: 524,881). The average sale stayed near 130, so changes came from the number of sales.
3. **Butchers earns the most per sale (139.12) and Milk Products the least (119.04).** This is the clearest difference in the data.
4. **Discounts do not increase sales.** The average sale is 130.49 with a discount and 129.95 without. Average quantity is 5.53 vs 5.58.
5. **Seasonality is weak.** Monthly revenue is fairly flat, with July strongest and February and October weakest.
6. **Customers are very even.** Each of the 25 customers spends between about 57,000 and 68,000.

## 5. Pivot Table: Top Items

A pivot table of revenue by item (200 items) shows the top sellers:

| Rank | Item | Revenue |
|---|---|---|
| 1 | Furniture (Item 25) | 25,625 |
| 2 | Electric household essentials (Item 25) | 25,502 |
| 3 | Butchers (Item 25) | 22,427 |
| 4 | Furniture (Item 24) | 22,080.5 |
| 5 | Food (Item 25) | 21,771 |

## 6. Recommendations

| Insight | Recommendation |
|---|---|
| Revenue is evenly spread | Focus on growing the whole business, not rescuing one area |
| 2024 recovery after the 2023 dip | Find out what drove 2024 and repeat it |
| Butchers leads, Milk Products trails | Promote Butchers, and review pricing or product mix in Milk Products |
| Discounts show no effect | Review whether discounts are worth their cost |
| Flat monthly pattern | Plan campaigns for the weaker months |
| Incomplete records | Record quantity, total and discount status for every sale |

## 7. Charts

Add your chart screenshots here:

1. Revenue by Year
2. Revenue by Category
3. Revenue by Location
4. Revenue by Payment Method
5. Average Sale by Category
6. Revenue by Month (2022 to 2024)
7. Top 10 Items by Revenue

## Limitations

- 604 sales (4.8%) have no value and are left out of revenue figures.
- 4,199 rows (33%) have an unknown discount status, so discount findings rely on the remaining 7,983 sales.
- 2025 has only 18 days of data, so it is excluded from year and month comparisons.
- Only 25 customers, so results may not represent a larger customer base.

## Skills Demonstrated

Data quality checking, data cleaning, exploratory analysis, pivot tables, charts, dashboards, business insight writing, and Google Sheets (SUMPRODUCT, SUMIF, AVERAGEIF, COUNTUNIQUE, ARRAYFORMULA, VLOOKUP).
