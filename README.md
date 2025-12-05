# Analyzing-Motorcycle-Part-Sales
Working on behalf of a company that sells motorcycle parts, I'll dig into their data to help them understand their revenue streams. I'll build up a query to find out how much net revenue they are generating across their product lines, segregating by date and warehouse.


SELECT product_line,
       TO_CHAR(date, 'Month') AS month,
       warehouse,
       SUM(total) - SUM(payment_fee) AS net_revenue
FROM sales
WHERE EXTRACT(MONTH FROM date) IN (6,7,8)
  AND client_type = 'Wholesale'
GROUP BY product_line, TO_CHAR(date, 'Month'), warehouse
ORDER BY product_line DESC, month DESC, net_revenue DESC;
