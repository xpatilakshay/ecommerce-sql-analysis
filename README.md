📊 Task 3 - SQL for Data Analysis
=================================

🚀 Internship: Data Analyst
---------------------------

This task demonstrates my ability to analyze structured e-commerce data using SQL. I’ve covered database creation, querying, subqueries, views, optimizations, and more.
SQL-based data analysis project using an e-commerce dataset. Includes database creation, analytical queries, subqueries, views, indexing, and performance optimization as part of a Data Analyst internship task.

🧠 What I Did
-------------
- Created a SQL database from an e-commerce CSV
- Wrote queries for filtering, aggregating, and analyzing data
- Used views and indexes for optimized analysis
- Answered common SQL interview questions

📁 Files Included
-----------------
- task3_queries.sql: All queries (database creation to advanced)
- E-commerce Dataset.csv: Data used
- screenshots/: Query results
- README.md: This file

📊 Dataset Overview
-------------------
The dataset includes:

- Order_Date, Time, Aging, Customer_Id, Gender, Device_Type
- Customer_Login_type, Product_Category, Product
- Sales, Quantity, Discount, Profit, Shipping_Cost
- Order_Priority, Payment_method

> Rows: 51,290

🧱 Database & Table Creation
----------------------------

CREATE DATABASE ecommerce_analysis;
USE ecommerce_analysis;

CREATE TABLE ecommerce_data (
    Order_Date DATE,
    Time TIME,
    Aging INT,
    Customer_Id INT,
    Gender VARCHAR(10),
    Device_Type VARCHAR(20),
    Customer_Login_type VARCHAR(20),
    Product_Category VARCHAR(100),
    Product VARCHAR(100),
    Sales FLOAT,
    Quantity FLOAT,
    Discount FLOAT,
    Profit FLOAT,
    Shipping_Cost FLOAT,
    Order_Priority VARCHAR(20),
    Payment_method VARCHAR(20)
);

📌 Queries
----------

-- Basic Queries

SELECT * FROM ecommerce_data LIMIT 10;

SELECT DISTINCT Product_Category FROM ecommerce_data;

SELECT * FROM ecommerce_data WHERE Gender = 'Female' AND Device_Type = 'Mobile';

SELECT * FROM ecommerce_data WHERE Order_Date LIKE '2018%';

SELECT * FROM ecommerce_data WHERE Order_Priority = 'High' AND Profit > 100;

-- Aggregations

SELECT Payment_method, SUM(Sales) FROM ecommerce_data GROUP BY Payment_method;

SELECT Customer_Login_type, COUNT(*) FROM ecommerce_data GROUP BY Customer_Login_type;

SELECT Product_Category, AVG(Discount) FROM ecommerce_data GROUP BY Product_Category;

SELECT Device_Type, SUM(Sales), AVG(Sales) FROM ecommerce_data GROUP BY Device_Type;

SELECT Product, SUM(Quantity) FROM ecommerce_data GROUP BY Product ORDER BY SUM(Quantity) DESC LIMIT 5;

-- Subqueries

SELECT * FROM ecommerce_data WHERE Sales > (SELECT AVG(Sales) FROM ecommerce_data);

-- Views

CREATE VIEW daily_profit_summary AS
SELECT Order_Date, SUM(Profit) AS Daily_Profit
FROM ecommerce_data
GROUP BY Order_Date;

-- Indexing

CREATE INDEX idx_customer_id ON ecommerce_data(Customer_Id);
CREATE INDEX idx_product_category ON ecommerce_data(Product_Category);
CREATE INDEX idx_order_date ON ecommerce_data(Order_Date);

-- Handling NULLs

SELECT * FROM ecommerce_data WHERE Shipping_Cost IS NULL;

SELECT COALESCE(Quantity, 0), COALESCE(Shipping_Cost, 0) FROM ecommerce_data;

-- Window Functions (PostgreSQL)

SELECT Order_Date, SUM(Sales) OVER (ORDER BY Order_Date) AS Cumulative_Sales FROM ecommerce_data;

SELECT Product, Profit, RANK() OVER (ORDER BY Profit DESC) AS Rank_By_Profit FROM ecommerce_data;

-- Advanced Metrics

SELECT AVG(user_sales) AS ARPU
FROM (
    SELECT Customer_Id, SUM(Sales) AS user_sales
    FROM ecommerce_data
    GROUP BY Customer_Id
) AS customer_sales;

❓ Interview Questions & Answers
-------------------------------

1. What is the difference between WHERE and HAVING?
   - WHERE filters rows before grouping.
   - HAVING filters groups after GROUP BY.

2. What are the different types of joins?
   - INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL OUTER JOIN

3. How do you calculate average revenue per user in SQL?
   Use a subquery to get SUM(Sales) per user, then average it:

   SELECT AVG(user_sales) FROM (
     SELECT Customer_Id, SUM(Sales) AS user_sales
     FROM ecommerce_data
     GROUP BY Customer_Id
   ) AS customer_sales;

4. What are subqueries?
   A query inside another query. Used to calculate or filter values dynamically.

5. How do you optimize a SQL query?
   - Use indexes
   - Avoid SELECT *
   - Use efficient filters and joins
   - Analyze query execution plan

6. What is a view in SQL?
   A virtual table based on the result-set of a query, created using CREATE VIEW.

7. How do you handle NULL values in SQL?
   - Use IS NULL, IS NOT NULL for checks
   - Use COALESCE() to replace with default


👋 About Me
-----------
- Instagram: https://instagram.com/xpatilakshay
