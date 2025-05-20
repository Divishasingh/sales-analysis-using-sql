
# 📊 Sales Trend Analysis Using SQL (500 Rows)

## 🎯 Objective
Analyze **monthly revenue** and **order volume** using SQL aggregation functions on a dataset of 500 randomly generated sales records.

---

## 🛠️ Tools Used
- [DB Fiddle (MySQL 8.0)](https://www.db-fiddle.com/)
- MySQL SQL Queries

---

## 🗃️ Dataset Description

**Table:** `orders`

| Column      | Type           | Description                         |
|-------------|----------------|-------------------------------------|
| order_id    | INT (AUTO_INCREMENT) | Unique ID for each order         |
| order_date  | DATE           | Date the order was placed           |
| product_id  | INT            | Product identifier (100–120)        |
| amount      | DECIMAL(10, 2) | Order revenue amount (₹50–₹1000)    |

A total of **500 records** were inserted with randomized data values across the year **2023**.

---

## 🧱 Schema & Data Generation Script

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY AUTO_INCREMENT,
    order_date DATE,
    product_id INT,
    amount DECIMAL(10, 2)
);

-- Insert 500 random orders
INSERT INTO orders (order_date, product_id, amount)
SELECT
    DATE_ADD('2023-01-01', INTERVAL FLOOR(RAND() * 365) DAY) AS order_date,
    FLOOR(100 + RAND() * 20) AS product_id,
    ROUND(50 + RAND() * 950, 2) AS amount
FROM
    (SELECT 1 UNION ALL SELECT 2 UNION ALL SELECT 3 UNION ALL SELECT 4 UNION ALL SELECT 5
     UNION ALL SELECT 6 UNION ALL SELECT 7 UNION ALL SELECT 8 UNION ALL SELECT 9 UNION ALL SELECT 10) AS t1
CROSS JOIN
    (SELECT 1 UNION ALL SELECT 2 UNION ALL SELECT 3 UNION ALL SELECT 4 UNION ALL SELECT 5
     UNION ALL SELECT 6 UNION ALL SELECT 7 UNION ALL SELECT 8 UNION ALL SELECT 9 UNION ALL SELECT 10) AS t2
CROSS JOIN
    (SELECT 1 UNION ALL SELECT 2 UNION ALL SELECT 3 UNION ALL SELECT 4 UNION ALL SELECT 5) AS t3
LIMIT 500;


##  Step 2: Run the Sales Trend Analysis Query

```sql
SELECT
    EXTRACT(YEAR FROM order_date) AS order_year,
    EXTRACT(MONTH FROM order_date) AS order_month,
    SUM(amount) AS total_revenue,
    COUNT(DISTINCT order_id) AS total_orders
FROM
    orders
GROUP BY
    order_year, order_month
ORDER BY
    order_year, order_month;
```

### 📈 Output Description

**Schema (MySQL v8)**

    -- Create orders table
    CREATE TABLE orders (
        order_id INT PRIMARY KEY AUTO_INCREMENT,
        order_date DATE,
        product_id INT,
        amount DECIMAL(10, 2)
    );
    
    -- Insert 500 rows using cross join of three derived tables with distinct aliases
    INSERT INTO orders (order_date, product_id, amount)
    SELECT
        DATE_ADD('2023-01-01', INTERVAL FLOOR(RAND() * 365) DAY) AS order_date,
        FLOOR(100 + RAND() * 20) AS product_id,   -- product ids between 100 and 120
        ROUND(50 + RAND() * 950, 2) AS amount     -- amounts between 50 and 1000
    FROM
        (SELECT 1 AS n UNION ALL SELECT 2 UNION ALL SELECT 3 UNION ALL SELECT 4 UNION ALL SELECT 5
         UNION ALL SELECT 6 UNION ALL SELECT 7 UNION ALL SELECT 8 UNION ALL SELECT 9 UNION ALL SELECT 10) AS t1
    CROSS JOIN
        (SELECT 1 AS n UNION ALL SELECT 2 UNION ALL SELECT 3 UNION ALL SELECT 4 UNION ALL SELECT 5
         UNION ALL SELECT 6 UNION ALL SELECT 7 UNION ALL SELECT 8 UNION ALL SELECT 9 UNION ALL SELECT 10) AS t2
    CROSS JOIN
        (SELECT 1 AS n UNION ALL SELECT 2 UNION ALL SELECT 3 UNION ALL SELECT 4 UNION ALL SELECT 5) AS t3
    LIMIT 500;
    
    

---

**Query #1**

    SELECT
        EXTRACT(YEAR FROM order_date) AS order_year,
        EXTRACT(MONTH FROM order_date) AS order_month,
        SUM(amount) AS total_revenue,
        COUNT(DISTINCT order_id) AS total_orders
    FROM
        orders
    GROUP BY
        order_year, order_month
    ORDER BY
        order_year, order_month;

### Output         

| order_year | order_month | total_revenue | total_orders |
| ---------- | ----------- | ------------- | ------------ |
| 2023       | 1           | 29245.97      | 51           |
| 2023       | 2           | 16018.95      | 34           |
| 2023       | 3           | 18598.70      | 37           |
| 2023       | 4           | 27930.39      | 50           |
| 2023       | 5           | 19682.83      | 36           |
| 2023       | 6           | 17847.51      | 32           |
| 2023       | 7           | 23808.34      | 45           |
| 2023       | 8           | 24028.83      | 44           |
| 2023       | 9           | 17811.77      | 36           |
| 2023       | 10          | 16149.21      | 28           |
| 2023       | 11          | 26761.61      | 55           |
| 2023       | 12          | 30649.73      | 52           |

---

[View on DB Fiddle](https://www.db-fiddle.com/f/j3DBaFqmsgYqfgiiDCL4SM/0)

### 📌 Key Learnings

-How to use GROUP BY with YEAR() and MONTH() functions for time-based analysis.
-Use of SUM() and COUNT(DISTINCT) for aggregations.
-Creating test data using SQL-only approaches without manual entry.
-Time-series breakdown of business KPIs like revenue and order volume.

### LINK -https://www.db-fiddle.com/f/j3DBaFqmsgYqfgiiDCL4SM/0  
