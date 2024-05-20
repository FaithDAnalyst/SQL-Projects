# Hobby Stores Customer Behavior Analysis with SQL 

CREATE TABLE store_data (row_id varchar, order_id Varchar, order_date Date,
						ship_date Date, ship_mode Varchar, customer_id Varchar,
						product_id Varchar, sales Numeric, discount Numeric);
						
						
CREATE TABLE master_customer (customer_id Varchar, customer_name Varchar, segment Varchar, 
			                  country Varchar, city Varchar, state Varchar, postal_code Int,
			                  region Varchar, age Int);
			  
			  
CREATE TABLE master_product (product_id Varchar, category Varchar, 
							 sub_category Varchar, product_name Varchar);
			  
						
SELECT *
FROM store_data;


SELECT *
FROM master_product;

SELECT *
FROM master_customer;
# How many unique customers, and products exist?
SELECT DISTINCT COUNT(customer_name) AS unique_customer_count
FROM master_customer;
-- Hobby Stores has 793 unique customers.

SELECT DISTINCT COUNT(sub_category) AS unique_product_count
FROM master_product;

-- Hobby Stores has 1,861 unique products that it offers.


# Using the WHERE CLAUSE, write a query that retrieves customer names who are 30 years old.

SELECT customer_name AS customers_aged_30, age
FROM master_customer
WHERE age = 30
LIMIT 3;
-- Hobby stores have 25 customers whose age is exactly 30 years.


# What is the total number of customers in each segment?

SELECT COUNT(segment) AS consumer_segment_count
FROM master_customer
WHERE segment = 'Consumer';
-- Hobby stores has 409 customers under its consumer category and this category made the highest purchase.

SELECT COUNT(segment) AS corporate_segment_count
FROM master_customer
WHERE segment = 'Corporate';
-- 236 of Hobby stores customers belong to the Corporate category

SELECT COUNT(segment) AS consumer_segment_count
FROM master_customer
WHERE segment = 'Home Office';
-- 146 of Hobby Stores customers belong to the Home Office segment


# What is the distribution of customer ages across different regions?

SELECT DISTINCT region, ROUND(AVG (age)) AS customer_age_distribution
FROM master_customer
GROUP BY region;

# Which customer segments made the most purchases?

SELECT master_customer.segment, ROUND(SUM(sales)) AS sales_by_segment
FROM store_data
INNER JOIN master_customer ON master_customer.customer_id = store_data.customer_id
GROUP BY segment;

# What product category makes the most sales?

SELECT master_product.category, ROUND(SUM(sales)) AS sales_by_category
FROM store_data
INNER JOIN master_product ON master_product.product_id = store_data.product_id
GROUP BY category;

SELECT product_name, category, ROUND((sales * discount)) AS sales_amount
FROM store_data
JOIN master_product
USING (product_id)
ORDER BY sales_amount ASC;

SELECT category, ROUND(SUM(sales * discount)) AS sales_amount
FROM store_data
JOIN master_product
USING (product_id)
WHERE (sales * discount) IS NOT NULL
GROUP BY category
ORDER BY sales_amount DESC;

SELECT category, ROUND(SUM(sales)) AS sales_amount
FROM store_data
JOIN master_product
USING (product_id)
GROUP BY category
ORDER BY sales_amount DESC;

