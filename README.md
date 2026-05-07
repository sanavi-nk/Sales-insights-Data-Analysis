# Sales Insights Data Analysis

Sales performance analysis using **MySQL** and **Power BI** to uncover revenue trends, top customers, top products, and sales quantities.

##  Tech Stack

MySQL - Data storage & querying 
Power BI Desktop - Visualization
Power Query - Data transformation
DAX - Calculated measures

## Data Analysis Process

1. Loaded raw data into MySQL
2. Wrote SQL queries to clean and explore data
3. Connected Power BI to MySQL
4. Transformed data in Power Query
5. Built relationships in Model view
6. Created DAX measures
7. Built dashboard


## Data Analysis Using SQL Queries

**Show all customer records**
```sql
SELECT * FROM customers;
```

**Show total number of customers**
```sql
SELECT count(*) FROM customers;
```

**Show transactions for Chennai market** *(market code: Mark001)*
```sql
SELECT * FROM transactions WHERE market_code = 'Mark001';
```

**Show distinct product codes sold in Chennai**
```sql
SELECT DISTINCT product_code FROM transactions WHERE market_code = 'Mark001';
```

**Show transactions where currency is US dollars**
```sql
SELECT * FROM transactions WHERE currency = 'USD';
```

**Show transactions in 2020 joined by date table**
```sql
SELECT transactions.*, date.*
FROM transactions
INNER JOIN date ON transactions.order_date = date.date
WHERE date.year = 2020;
```

**Show total revenue in year 2020**
```sql
SELECT SUM(transactions.sales_amount)
FROM transactions
INNER JOIN date ON transactions.order_date = date.date
WHERE date.year = 2020;
```

**Show total revenue in January 2020**
```sql
SELECT SUM(transactions.sales_amount)
FROM transactions
INNER JOIN date ON transactions.order_date = date.date
WHERE date.year = 2020 AND date.month_name = 'January';
```

**Show total revenue in 2020 for Chennai**
```sql
SELECT SUM(transactions.sales_amount)
FROM transactions
INNER JOIN date ON transactions.order_date = date.date
WHERE date.year = 2020 AND transactions.market_code = 'Mark001';
```

---

## Data Analysis Using Power BI

**Formula to create `salesamount_in_lkr` column (Power Query)**

```m
= Table.AddColumn(
    #"Filtered currency INR",
    "salesamount_in_lkr",
    each
        if [currency] = "USD" then [sales_amount] * 319.34
        else if [currency] = "INR" then [sales_amount] * 3.38
        else null
)
```

> This converts all sales amounts to **Sri Lankan Rupees (LKR)** based on the transaction currency.

---

## Dashboard Features

-  **Total Revenue in LKR**
-  **Revenue Trend** over time
-  **Sales Quantity**
-  **Revenue by Market Name**
-  **Sales Quantity by Market Name**

> All metrics are filterable by **Year** and **Month**

---

##  Repository Structure

```
├── sales_insights.pbix       # Power BI report file
├── db_dump.sql               # MySQL database dump
├── README.md                 # Project documentation
└── screenshots/
    └── dashboard.png         # Dashboard preview
```

---

## How to Run

1. Import `db_dump.sql` into your MySQL server
2. Open `sales_insights.pbix` in Power BI Desktop
3. Update the MySQL connection string to point to your local server
4. Click **Refresh** to load the data

---
## Dashboard of PowerBI
<img width="1336" height="761" alt="Screenshot 2026-05-07 154458" src="https://github.com/user-attachments/assets/9219718c-621e-4512-9a4f-9e8bd940838e" />
