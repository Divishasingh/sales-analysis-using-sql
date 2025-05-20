
# Sales Trend Analysis Using SQL Aggregations

## Objective
Analyze monthly revenue and order volume from sales data using SQL aggregation functions and date extraction.

## Tools Used
- DB Fiddle (https://www.db-fiddle.com/)
- MySQL 8.0

  ## Files in this Project

* `setup_database.sql`: Contains the `CREATE TABLE` statement for the `orders` table and `INSERT` statements for sample data.
* `sales_analysis.sql`: Contains the SQL query to perform the monthly sales trend analysis.


## Dataset Description
The dataset consists of an `orders` table with the following columns:

| Column      | Type           | Description                    |
|-------------|----------------|-------------------------------|
| order_id    | INT (Primary Key) | Unique identifier for each order |
| order_date  | DATE           | Date when the order was placed |
| product_id  | INT            | Identifier for the product ordered |
| amount      | DECIMAL(10,2)  | Revenue amount for the order   |

## Sample Data
The sample dataset contains 50 rows with order data across multiple months in the year 2023, representing various products and revenue amounts.

## How to Run the Analysis

Follow these steps to set up your database and run the sales trend analysis query:

### Step 1: Set up the Database and Populate Data

 -- Create table
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    order_date DATE,
    product_id INT,
    amount DECIMAL(10, 2)
);

-- Insert 50 rows of sample data
INSERT INTO orders (order_id, order_date, product_id, amount) VALUES
(1, '2023-01-02', 101, 200.00),
(2, '2023-01-05', 102, 150.00),
(3, '2023-01-12', 103, 300.00),
(4, '2023-01-22', 104, 400.00),
(5, '2023-02-01', 101, 250.00),
(6, '2023-02-10', 105, 150.00),
(7, '2023-02-18', 106, 500.00),
(8, '2023-02-25', 107, 300.00),
(9, '2023-03-02', 108, 100.00),
(10, '2023-03-06', 102, 200.00),
(11, '2023-03-12', 103, 350.00),
(12, '2023-03-20', 109, 400.00),
(13, '2023-04-01', 101, 600.00),
(14, '2023-04-07', 104, 700.00),
(15, '2023-04-15', 110, 800.00),
(16, '2023-04-22', 111, 300.00),
(17, '2023-05-03', 101, 500.00),
(18, '2023-05-08', 102, 600.00),
(19, '2023-05-17', 104, 700.00),
(20, '2023-05-27', 107, 800.00),
(21, '2023-06-01', 108, 900.00),
(22, '2023-06-04', 105, 150.00),
(23, '2023-06-10', 103, 250.00),
(24, '2023-06-15', 111, 300.00),
(25, '2023-06-21', 109, 400.00),
(26, '2023-07-02', 101, 550.00),
(27, '2023-07-09', 104, 650.00),
(28, '2023-07-12', 102, 750.00),
(29, '2023-07-19', 107, 850.00),
(30, '2023-07-25', 108, 950.00),
(31, '2023-08-03', 109, 1050.00),
(32, '2023-08-07', 110, 1150.00),
(33, '2023-08-15', 101, 1250.00),
(34, '2023-08-22', 102, 1350.00),
(35, '2023-09-01', 103, 1450.00),
(36, '2023-09-05', 104, 1550.00),
(37, '2023-09-12', 105, 1650.00),
(38, '2023-09-20', 106, 1750.00),
(39, '2023-10-01', 107, 1850.00),
(40, '2023-10-09', 108, 1950.00),
(41, '2023-10-18', 109, 2050.00),
(42, '2023-10-25', 110, 2150.00),
(43, '2023-11-03', 111, 2250.00),
(44, '2023-11-08', 101, 2350.00),
(45, '2023-11-15', 102, 2450.00),
(46, '2023-11-23', 103, 2550.00),
(47, '2023-12-01', 104, 2650.00),
(48, '2023-12-10', 105, 2750.00),
(49, '2023-12-20', 106, 2850.00),
(50, '2023-12-28', 107, 2950.00);


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

## Expected Output

After successfully running the `sales_analysis.sql` query on the provided `orders` table, you will receive a results table similar to the one below. This table displays the aggregated `total_revenue` and `total_orders` (volume) for each month in the dataset, ordered chronologically.
  
