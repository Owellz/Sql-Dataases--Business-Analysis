# Sql-Dataases--Business-Analysis


-- joining tables of two different tables within the databases. 
-- aim here is to find payment methods used by customers with there respective imvoice id
--- 
SELECT
p.date,
p.invoice_id,
p.amount,
c.name,
pm.name 
FROM
payments p
join clients c
on p.client_id = c.client_id
join payment_methods pm
on pm.payment_method_id = p.payment_method



----- joining table across three tables
--- aim is to find the status of orders either they have been shipped or still being processed. 
--- customers table, order status table and order tables were INNER JOIN 

SELECT 
o.order_id,
o.order_date,
c.first_name,
c.last_name,
name AS Status 
FROM 
orders o
JOIN customers c
ON o.customer_id = c.customer_id
JOIN order_statuses os
ON os.order_status_id = o.status

-- joining tables to it self by using SELF join

SELECT 
e.employee_id,
e.first_name,
m.first_name AS Manager
FROM 
employees e
JOIN employees m
ON e.reports_to = m.employee_id;
