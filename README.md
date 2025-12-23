# SQL-Retail_Sales

SQL Retail Sales Analysis Project
This README documents a comprehensive SQL analysis project on retail sales data, covering data exploration, cleaning, and business intelligence queries for key performance insights.
​

Project Overview
The project analyzes retail sales transactions stored in the retail_sales table, addressing 10 business-critical questions ranging from basic filtering to advanced analytics like ranking best-selling months and customer segmentation by shifts. It demonstrates SQL skills in aggregation, window functions, date manipulations, and CTEs, suitable for BCA Data Science portfolios and internship applications.
​

Table Schema
The core table retail_sales captures transaction details with the following structure:
​

Column	Data Type	Description
transactions_id	INT (PK)	Unique transaction identifier
​
sale_date	DATE	Date of sale
​
sale_time	TIME	Time of sale
​
customer_id	INT	Customer identifier
​
gender	VARCHAR(20)	Customer gender
​
age	INT	Customer age
​
category	VARCHAR(20)	Product category
​
quantiy	INT	Quantity sold
​
price_per_unit	FLOAT	Price per unit
​
cogs	FLOAT	Cost of goods sold
​
total_sale	FLOAT	Total sale amount
​
Setup Instructions
Create the table using the provided DDL script in the SQL file.
​

Load your retail sales dataset into the retail_sales table (CSV import recommended via tools like pgAdmin or MySQL Workbench).
​

Execute data quality checks for NULL values before analysis.
​

Run exploration queries to validate record counts, unique customers, and categories.
​

Sample Table Creation Code:

sql
CREATE TABLE retail_sales (
    transactions_id INT PRIMARY KEY,
    sale_date DATE,
    sale_time TIME,
    customer_id INT,
    gender VARCHAR(20),
    age INT,
    category VARCHAR(20),
    quantiy INT,
    price_per_unit FLOAT,
    cogs FLOAT,
    total_sale FLOAT
);
Key Analyses Performed
The project solves 10 business questions with production-ready SQL queries:
​

Data Exploration: Total sales count, unique customers, distinct categories.
​

Q1: Sales on specific date (2022-11-05).
​

Q2: Clothing transactions >3 units in Nov-2022.
​

Q3: Total sales and orders by category.
​

Q4: Average age of Beauty category buyers.
​

Q5: High-value transactions (>1000).
​

Q6: Transactions by gender and category.
​

Q7: Best-selling month per year using RANK() window function.
​

Q8: Top 5 customers by total sales.
​

Q9: Unique customers per category.
​

Q10: Orders by time shift (Morning/Afternoon/Evening) using CTE and CASE.
​

Featured Advanced Query (Q7 - Best Selling Month):

sql
SELECT year, month, avg_sale
FROM (
    SELECT
        EXTRACT(YEAR FROM sale_date) as year,
        EXTRACT(MONTH FROM sale_date) as month,
        AVG(total_sale) as avg_sale,
        RANK() OVER(PARTITION BY EXTRACT(YEAR FROM sale_date) 
                    ORDER BY AVG(total_sale) DESC) AS rank
    FROM retail_sales
    GROUP BY 1, 2
) as t1
WHERE rank = 1;
Usage Notes
Compatible with PostgreSQL (uses EXTRACT, TO_CHAR, RANK()).
​

Assumes clean data post-NULL checks; add data loading script for production.
​

Extend by joining customer demographics or inventory tables for deeper insights.
​

Full SQL Code
The complete script is in SQL-Retail-Sales-Analysis.sql, including table creation, data validation, exploration, and all 10 query solutions.
​
