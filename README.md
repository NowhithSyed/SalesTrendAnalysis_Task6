# SalesTrendAnalysis_Task6
SQL-based analysis of online sales data to track monthly performance, identify seasonal trends, and highlight top revenue months.
# Task 6 – Sales Trend Analysis

## Objective
Analyze monthly revenue and order volume from the `online_sales` dataset using SQL aggregation functions.

## Dataset
- Columns: `order_id`, `product_id`, `order_date`, `amount`
- Format: CSV (imported into MySQL)

## Steps
1. Created database and `orders` table.
2. Imported CSV data using MySQL Workbench .
3. Used `EXTRACT()` and `DATE_FORMAT()` to group by year/month.
4. Calculated:
   - Monthly Revenue → `SUM(amount)`
   - Order Volume → `COUNT(DISTINCT order_id)`
5. Ordered results chronologically and limited to top months.

## Key Queries
```sql
-- Monthly Revenue & Volume
SELECT
    EXTRACT(YEAR FROM order_date) AS year,
    EXTRACT(MONTH FROM order_date) AS month,
    SUM(amount) AS monthly_revenue,
    COUNT(DISTINCT order_id) AS order_volume
FROM online_sales
GROUP BY year, month
ORDER BY year, month;

-- Top 3 Months by Revenue
SELECT
    DATE_FORMAT(order_date, '%Y-%m') AS year_month,
    SUM(amount) AS monthly_revenue
FROM online_sales
GROUP BY DATE_FORMAT(order_date, '%Y-%m')
ORDER BY monthly_revenue DESC
LIMIT 3;
