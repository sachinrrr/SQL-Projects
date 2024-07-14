-- 1.Retrieve all customer names and their corresponding email addresses.
SELECT
first_name,
last_name,
email
FROM customers;

-- 2.List all products along with their brand names and categories.
SELECT
product_name,
brand_name,
category_name
FROM products p INNER JOIN brands b
ON p.brand_id = b.brand_id
INNER JOIN category c
ON P.category_id = c.category_id;

-- 3.Show all orders along with the customer details who placed them.
SELECT
order_id,
order_date,
shipped_date,
CONCAT(first_name, " ",last_name) AS CustomerName,
phone,
email
FROM orders o INNER JOIN customers c
ON o.customer_id = c.customer_id;

 -- 4.Find the total number of orders placed by each customer.
SELECT 
o.customer_id,
CONCAT(c.first_name," ",c.last_name) AS Customer_name, 
COUNT(order_id) AS total_orders 
FROM Orders o INNER JOIN customers c
On o.customer_id = c.customer_id
GROUP BY customer_id
ORDER BY customer_id;

-- 5.Calculate the average list price of products in each category.
SELECT
c.category_name,
AVG(p.list_price) AS average_price
FROM products p INNER JOIN category c
ON p.category_id = c.category_id
GROUP BY c.category_name;

-- 6.Determine the total quantity of each product available in all stores.
SELECT 
product_id, 
SUM(quantity) AS total_quantity 
FROM Stocks 
GROUP BY product_id;

-- 7.Retrieve the order details along with the product names for all orders.
SELECT 
o.order_id,
p.product_name,
o.quantity,
o.list_price,
o.discount
FROM orderdetails o INNER JOIN products p
ON o.product_id = p.product_id;

-- 8.List all customers along with the total amount they have spent.
SELECT
CONCAT(c.first_name, " ", c.last_name) AS Customer_name,
(od.list_price * od.quantity) - od.discount AS Spent_amount
FROM customers c INNER JOIN orders o
ON c.customer_id = o.customer_id
INNER JOIN orderdetails od
ON o.order_id = od.order_id
ORDER BY Spent_amount;

-- 9. Show the details of products that have never been ordered.
SELECT 
p.product_id, 
p.product_name, 
p.list_price
FROM Products p LEFT JOIN Orderdetails od 
ON p.product_id = od.product_id
WHERE od.product_id IS NULL;

-- 10. List the top 3 customers who have spent the most money.
SELECT
CONCAT(c.first_name, " ", c.last_name) AS Customer_name,
(od.list_price * od.quantity) - od.discount AS Top3_highest_spent_amounts
FROM customers c INNER JOIN orders o
ON c.customer_id = o.customer_id
INNER JOIN orderdetails od
ON o.order_id = od.order_id
ORDER BY Top3_highest_spent_amounts DESC
LIMIT 3;

-- 11. Identify the most frequently ordered product.
SELECT
p.product_name,
COUNT(od.product_id) AS order_count
FROM orderdetails od INNER JOIN products p
ON p.product_id = od.product_id
GROUP BY p.product_id
ORDER BY order_count DESC
LIMIT 1;

-- 12. Find the products that have been ordered by at least 10 different customers.
SELECT 
od.product_id,
p.product_name,
COUNT(DISTINCT o.customer_id) AS customer_count
FROM Orderdetails od INNER JOIN Orders o 
ON od.order_id = o.order_id
INNER JOIN Products p 
ON od.product_id = p.product_id
GROUP BY od.product_id, p.product_name
HAVING COUNT(DISTINCT o.customer_id) >= 10;

-- 13. Add a new customer to the Customers table.
INSERT INTO customers VALUES
(1446, "John", "Doe", "(716) 946-3195", "john.doe@example.com", "123 Elm St", "Chicago", "IL", 60601);

-- 14. Update the email address of a customer id 1256.
UPDATE customers
SET email = "nubia5.anderson@gmail.com"
WHERE customer_id = 1256;

-- 15. Delete all orders placed by a specific customer.
DELETE 
FROM orders 
WHERE customer_id = 2;

-- 16. Find the top 5 products with the highest total sales amount.
SELECT
od.product_id,
p.product_name,
SUM(od.quantity * (od.list_price - od.discount)) AS total_sales
FROM orderdetails od INNER JOIN products p
ON od.product_id = p.product_id
GROUP BY od.product_id
ORDER BY total_sales DESC
LIMIT 5;

-- 17. Retrieve the details of orders that were shipped more than 2 days after the order date.
SELECT
order_id,
order_date,
shipped_date
FROM Orders
WHERE DATEDIFF(shipped_date, order_date) > 2;

-- 18. Retrieve the details of orders with a total amount greater than $500.
SELECT
o.order_id,
o.order_date,
SUM(od.quantity * (od.list_price - od.discount)) AS total_amount
FROM Orders o INNER JOIN Orderdetails od 
ON o.order_id = od.order_id
GROUP BY o.order_id, o.order_date
HAVING total_amount > 500;

-- 19. Calculate the total discount given on all orders.
SELECT
order_id,
SUM(discount * quantity) AS total_discount
FROM Orderdetails
GROUP BY order_id;

-- 20. Find the customers who have never placed an order.
SELECT
c.customer_id,
c.first_name,
c.last_name 
FROM Customers c
WHERE c.customer_id NOT IN (SELECT DISTINCT 
			    o.customer_id 
			    FROM Orders o);
