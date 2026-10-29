# Amazon India Apparel Sales Dashboard (Excel)

An Excel dashboard analysing ~108,000 order lines from an apparel seller on Amazon India, covering 31 March to 29 June 2022. It answers three questions: which products drive revenue, where customers are, and how sales moved week to week.

![Dashboard Preview](dashboard-preview.png)

## Key Findings

- **Two categories carry the business.** Sets (49.9%) and Kurtas (27.1%) bring in 77% of the ₹71.7M gross revenue. The bottom five categories together are under 2%.
- **Sales are concentrated in a few states.** Maharashtra (₹12.2M) and Karnataka (₹9.6M) alone account for about 31% of revenue.
- **Sales dropped sharply in early May and never fully recovered.** Weekly revenue held around ₹6.3M through the week of 2 May, then fell 27% the next week to ₹4.8M. It climbed back to ₹5.9M by early June before sliding again, so the last four weeks averaged 14% below the first four.
- **Most orders are single items.** 100,727 orders contained 108,483 units, about 1.08 units per order, with an average order value of ₹712.
- **Returns are low, but many orders were still open.** Only 1.9% of order lines were returned, but 71% were still in transit when the data was pulled, so the final return rate is likely higher.

## Data

- **Source:** Kaggle "Amazon Sale Report" (Amazon India e-commerce sales, 2022).
- **Scope:** Cancelled orders excluded. Revenue is the gross value of all remaining orders, including returns.
- **Note on dates:** the dataset starts on 31 March and ends on 29 June, so the weekly trend only shows the 12 full Monday–Sunday weeks (4 Apr – 26 Jun). The partial days are still included in the totals.

## Cleaning Steps

- Filled 26 blank `State` values with "Unknown"
- Grouped detailed order statuses into four buckets: In Transit, Delivered, Returned, Other
- Added `Month` and `Week_Start` (Monday of the order's week) columns from the order date
- Kept 7,344 repeated Order IDs, since these are multi-item orders (one row per product)
- Added an `Is_First_Line` flag so the dashboard counts **unique orders** (100,727) rather than order lines (108,071)

## How It's Built

| Sheet | What it does |
|---|---|
| **Dashboard** | KPI cards and four charts (weekly trend, category, state, order status) |
| **Summary Tables** | Revenue, orders and units by month, week, category, state and status, plus KPI calculations |
| **Category x Month** | Revenue matrix by category and month built with `SUMIFS`, with average revenue per line |
| **PivotTable** | Native Excel PivotTable of revenue by category and month, built from the same data as a cross-check |
| **Clean Data** | The cleaned dataset as an Excel Table, plus cleaning notes |

All numbers are live formulas (`SUMIFS`, `COUNTIFS`, `AVERAGEIF`, `IF`) built on the Excel Table, so the dashboard updates if the data changes. The **PivotTable** sheet rebuilds the category × month view with a native PivotTable, and its totals match the formula tables exactly (₹71,673,394), a quick way to confirm the formulas are right. On the dashboard, the five smallest categories are grouped as "Other" (2% of revenue together) so the chart stays readable. The category and state lists are fixed to the top items at the time of analysis.

## Skills Demonstrated

Data cleaning · Excel Tables and structured references · SUMIFS / COUNTIFS · PivotTables · KPI design · Dashboard layout · Data visualisation

## Files

- `Amazon_Dashboard_Final.xlsx`: full workbook (dashboard, summary tables, PivotTable and cleaned data)
- `dashboard-preview.png`: dashboard screenshot
