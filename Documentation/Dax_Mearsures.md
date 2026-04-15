# 📊 DAX Measures Documentation

This document outlines the key DAX measures used in the **E-Commerce Sales Analytics Power BI Dashboard**. These measures help analyze sales performance, customer behavior, and year-over-year trends.

---

## 🧾 1. Total Sales
Calculates the total revenue generated from all transactions.

```DAX
Total Sales = SUM(fact_table[total_price])

📦 2. Total Quantity

Represents the total number of units sold.

Total Quantity = SUM(fact_table[quantity])

💰 3. Average Unit Price (ASP)

Calculates the average selling price per unit.

Average Unit Price = DIVIDE([Total Sales], [Total Quantity])

📅 4. Previous Year Sales (PY Sales)

Returns the total sales for the same period in the previous year.

PY Sales =
CALCULATE(
    [Total Sales],
    SAMEPERIODLASTYEAR(time_dim[Date])
)

📈 5. Year-over-Year (YoY) Sales %

Measures the percentage growth or decline in sales compared to the previous year.

YoY % Sales =
VAR Growth =
    DIVIDE([Total Sales] - [PY Sales], [PY Sales])
RETURN
    Growth

📦 6. Previous Year Quantity

Calculates the total quantity sold in the previous year.

PY Quantity =
CALCULATE(
    [Total Quantity],
    SAMEPERIODLASTYEAR(time_dim[Date])
)

📊 7. Year-over-Year (YoY) Quantity %

Measures the percentage change in quantity sold compared to the previous year.

YoY % Quantity =
VAR Growth =
    DIVIDE([Total Quantity] - [PY Quantity], [PY Quantity])
RETURN
    Growth

💵 8. Previous Year Average Unit Price

Calculates the average unit price for the previous year.

PY Average Unit Price =
CALCULATE(
    [Average Unit Price],
    SAMEPERIODLASTYEAR(time_dim[Date])
)

📉 9. Year-over-Year (YoY) Average Unit Price %

Measures the percentage change in average unit price compared to the previous year.

YoY % Avg Unit Price =
VAR Growth =
    DIVIDE(
        [Average Unit Price] - [PY Average Unit Price],
        [PY Average Unit Price]
    )
RETURN
    Growth

👥 10. Total Customers

Counts the number of unique customers.

Total Customers = DISTINCTCOUNT(customer_dim[customer_id])

🟢 11. Active Customers

Counts customers who have made at least one purchase.

Active Customers = DISTINCTCOUNT(fact_table[customer_id])

🔁 12. Returning Customers

Counts customers who have made more than one purchase.

Returning Customers =
CALCULATE(
    DISTINCTCOUNT(fact_table[customer_id]),
    FILTER(
        VALUES(fact_table[customer_id]),
        CALCULATE(COUNT(fact_table[transaction_id])) > 1
    )
)

🔄 13. Returning Customers %

Calculates the percentage of returning customers.

Returning Customers % =
DIVIDE([Returning Customers], [Total Customers], 0)

🛒 14. Order Count

Represents the total number of transactions.

Order Count = DISTINCTCOUNT(fact_table[transaction_id])

🏆 15. Top N Products by Quantity

Ranks products based on the quantity sold.

Product Rank =
RANKX(
    ALL(item_dim[item_name]),
    [Total Quantity],
    ,
    DESC,
    DENSE
)

📍 16. Total Sales by Location

Calculates total sales for each store/location.

Total Sales by Location = [Total Sales]

📅 17. Year-to-Date (YTD) Sales

Calculates cumulative sales from the beginning of the year to the current date.

YTD Sales =
TOTALYTD(
    [Total Sales],
    time_dim[Date]
)


🛠️ Tools Used

Power BI Desktop
DAX (Data Analysis Expressions)
Power Query for Data Transformation

