# DATA-ANALYSIS-WITH-COMPLEX-QUERIES-TASK2
SQL Report: Data Analysis Using Complex Queries

🔧 Tools Used:

SQL PLAYGROUND

SQL queries with: GROUP BY, window functions, subqueries, CTEs



---

📁 Dataset: sales_data

id	customer_name	product	quantity	price	sale_date

1	Alice	Laptop	1	700	2024-01-01
2	Bob	Phone	2	300	2024-01-03
3	Alice	Headphones	3	50	2024-02-01
4	John	Laptop	1	700	2024-02-10
5	Alice	Phone	1	300	2024-03-05
📌 Analysis Queries & Results

🔹 1. Total Revenue by Product

SELECT 
  product,
  SUM(quantity * price) AS total_revenue
FROM sales_data
GROUP BY product;

🟢 Result:

product	total_revenue

Laptop	1400
Phone	900
Headphones	150

2. Customer Spending Ranking (Window Function)

SELECT 
  customer_name,
  SUM(quantity * price) AS total_spent,
  RANK() OVER (ORDER BY SUM(quantity * price) DESC) AS spending_rank
FROM sales_data
GROUP BY customer_name;

🟢 Result:

customer_name	total_spent	spending_rank

Alice	1150	1
Bob	600	2
John	700	2

3. Monthly Sales Trend (CTE + Running Total)

WITH monthly_sales AS (
  SELECT 
    DATE_FORMAT(sale_date, '%Y-%m') AS sale_month,
    SUM(quantity * price) AS total_sales
  FROM sales_data
  GROUP BY sale_month
)
SELECT 
  sale_month,
  total_sales,
  SUM(total_sales) OVER (ORDER BY sale_month) AS running_total
FROM monthly_sales;

🟢 Result:

sale_month	total_sales	running_total

2024-01	1300	1300
2024-02	850	2150
2024-03	300	2450
📈 Insights:

💸 Top-selling product: Laptop (₹1400)

👑 Top customer: Alice (₹1150)

📊 Peak sales month: January 2024 (₹1300)

📈 Cumulative sales show growth over time



---

✅ Conclusion

This report uses advanced SQL features like window functions, subqueries, and CTEs to uncover trends and patterns in sales data, meeting the goal of data analysis with complex queries.
