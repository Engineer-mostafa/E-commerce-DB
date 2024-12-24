# 🌴 E-Commerce System (from Practical Web Database Design Book)

This repository contains the analysis and design for the **Database** based on the book **"Practical Web Database Design"**. 

## 📖 Table of Contents

- [📋 ERD](#-erd-diagram)
- [🌐 Some Quesries](#-queries)
- [🎭 Relationships Between Tables](#-relationships)


## 📋 ERD Diagram
![E-Commerce-erd](https://github.com/user-attachments/assets/c2ad3e4a-e8f2-4762-b94d-e4bc6d499ccc)


## 🌐 Queries
Write an SQL query to generate a daily report of the total revenue for a specific date.
```
SELECT  ORDER.order_date AS report_date,sum(ORDER.total_amount) as Total_Revenue
from `order` 
where ORDER.order_date = '2024-12-03';
```

Write an SQL query to generate a monthly report of the top-selling products in a given month.
```
SELECT 
    p.name AS product_name,
    SUM(od.quantity) AS total_quantity_sold,
    SUM(od.quantity * od.unit_price) AS total_revenue
FROM 
    order_details od
JOIN 
    `order` o ON od.order_id = o.order_id
JOIN 
    product p ON od.product_id = p.product_id
WHERE 
    DATE_FORMAT(o.order_date, '%Y-%m') = '2024-12'
GROUP BY 
    p.product_id
ORDER BY 
    total_quantity_sold DESC
```

Write a SQL query to retrieve a list of customers who have placed orders totaling more than $500 in the past month.
Include customer names and their total order amounts.
```
SELECT 
    CONCAT(c.first_name," ",c.last_name ) AS Customer_Name,
    sum(o.total_amount) as total_order_amount
FROM 
    customer c
JOIN 
  `order` o on c.customer_id = o.customer_id 
GROUP BY 
	c.customer_id
HAVING 
	total_order_amount > 500.0
ORDER BY 
    total_order_amount DESC;
```

## 🎭 Relationships
```
Ref: category.category_id < product.product_id // one-to-many

Ref: customer.customer_id < order.order_id // one-to-many

Ref: product.product_id < order_details.order_details_id // one-to-many

Ref: order.order_id < order_details.order_details_id // one-to-many
```

