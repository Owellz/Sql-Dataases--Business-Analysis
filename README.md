



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
os.name AS Status
name AS Status 
FROM 
orders o
JOIN customers c
ON o.customer_id = c.customer_id
JOIN order_statuses os
ON os.order_status_id = o.status

-- joining tables to it self by using SELF join

SELECT 
-- the employee and names must be prefix because they have different column
e.employee_id,
e.first_name,
m.first_name AS Manager
FROM 
employees e
JOIN employees m
ON e.reports_to = m.employee_id;


-- joining two tables having different databases

SELECT * 
FROM
order_items oi
-- to join table across different databases, you must prefix the table that is 
-- joining with by prefixing it with the name of the databases which is "product"
join sql_inventory.products p
on oi.product_id = p.product_id

-- Using A compound join condition to retrieve data use;--

SELECT 
* 
FROM 
order_items oi
JOIN order_item_notes oin
ON oi.order_id = oin.order_id
-- compound join condition--
AND oi.product_id = oin.product_id

-- Using LEFT JOIN to retrieve data whether a stated condition is true or not.--

SELECT 
*
FROM 
products p
-- using left join to retrive quantity of the products 
-- whether this condition = product id and order id is true or not.
LEFT JOIN order_items oi
ON p.product_id = oi.product_id


-- aim is to retrieve orders that have been shipped and whose status is known--

SELECT 
c.first_name AS Customer,
o.order_id,
o.order_date,
os.name AS Status,
sh.name AS Shipper
FROM 
orders o
JOIN customers c
ON c.customer_id = o.customer_id
LEFT JOIN shippers sh
ON o.shipper_id = sh.shipper_id
JOIN order_statuses os
ON o.status = os.order_status_id
