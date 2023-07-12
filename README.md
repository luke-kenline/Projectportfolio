**Overview**
This is a highlight of my abilities and prociency in SQL! In this example, I am analyzing customer revenue changes over time to detect customer behavior. The goal of highlighting this example is to highlight my comfortability with window functions, aggregating data and subquries.

**Query**

WITH revenue_data AS (
  SELECT
    customer_id,
    order_date,
    revenue,
    SUM(revenue) OVER (PARTITION BY customer_id ORDER BY order_date) AS cumulative_revenue,
    LAG(revenue) OVER (PARTITION BY customer_id ORDER BY order_date) AS previous_revenue
  FROM
    orders
)

SELECT
  customer_id,
  order_date,
  revenue,
  cumulative_revenue,
  revenue - previous_revenue AS revenue_change
FROM
  revenue_data
ORDER BY
  customer_id,
  order_date;

**Explained:**
1. The query begins with a CTE named revenue_data. The CTE retrieves data from the orders table and calculates three window functions: SUM() OVER, LAG() OVER. The SUM() OVER function calculates the cumulative revenue for each customer by ordering the records by the order date. The LAG() OVER function retrieves the previous revenue for each customer based on the order date.

The main query selects the columns customer_id, order_date, revenue, cumulative_revenue, and revenue_change from the revenue_data CTE.

The revenue_change column calculates the difference between the current revenue and the previous revenue for each customer. This helps identify how much the revenue has changed from one order to the next.

The results are ordered by customer_id and order_date to maintain a chronological order for each customer's transactions.
