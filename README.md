
CREATE TABLE retail_sales
	
( 
"transactions_id"  INT PRIMARY KEY,
	sale_date DATE,
	sale_time TIME,
	customer_id INT,
	gender VARCHAR(10),
	age INT,
	category VARCHAR (15),
	quantiy INT,
   price_per_unit FLOAT,	
     cogs	FLOAT,
      total_sale FLOAT
);

SELECT *
    
FROM retail_sales;

--  DATA CLEANING ----

SELECT * FROM retail_sales
WHERE transactions_id IS NULL

SELECT * FROM retail_sales
WHERE sale_date IS NULL

SELECT * FROM retail_sales
WHERE sale_time IS NULL

	
SELECT(*) FROM retail_sales
WHERE 
    transactions_id IS NULL
    OR
    sale_date IS NULL
    OR 
    sale_time IS NULL
    OR
    gender IS NULL
    OR
    category IS NULL
    OR
    quantiy IS NULL
    OR
    cogs IS NULL
    OR
    total_sale IS NULL;

DELETE FROM retail_sales
WHERE 
    transactions_id IS NULL
    OR
    sale_date IS NULL
    OR 
    sale_time IS NULL
    OR
    gender IS NULL
    OR
    category IS NULL
    OR
    quantiy IS NULL
    OR
    cogs IS NULL
    OR
    total_sale IS NULL;

--  DATA EXPLORATION---

 -- How many sales we have ?

 select count (*) as total_sales from retail_sales;

--  how many unique customers we have?

 select count( DISTINCT customer_id) as total_customer from retail_sales;


-- how many categories we have ?

 select distinct category from retail_sales;

-- Data Analysis & Business Key Problems & Answers


-- Q.1 Write a SQL query to retrieve all columns for sales made on '2023-05-15'.

 select * from retail_sales
 where sale_date =  '2023-05-15'

-- -- Q.2 Write a SQL query to retrieve all transactions where the category is
-- 'Clothing' and the quantity sold is more than 4 in the month of Nov-2022 
  

  select *
  from retail_sales
  where category = 'Clothing'
  and quantiy >= 4
  AND sale_date BETWEEN '2022-11-01' AND '2022-11-30';

-- Q.3 Write a SQL query to calculate the total sales (total_sale) for each category.

   select category,
	   sum(total_sale) as net_sales
	   from retail_sales
     group by  1;

-- Q.4 Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.

 select  ROUND( AVG(age), 2), as AVERAGE_AGE
 from retail_sales
 WHERE category = 'Beauty';


-- Q.5 Write a SQL query to find all transactions where the total_sale is greater than 1000.

  select * from retail_sales
  where total_sale >1000;


-- Q.6 Write a SQL query to find the total number of transactions (transaction_id) made by
-- each gender in each category.

  select 
 gender , category,
	  count (transactions_id ) as Total_trans
 from retail_sales
GROUP BY gender, category
order by 1;


-- -- Q.7 Write a SQL query to calculate the average sale for each month. 
-- Find out best selling month in each year
 
  select 
 extract ( YEAR FROM sale_date ) as year,
 extract ( MONTH FROM sale_date) as month,
 avg (total_sale) as avg_sale
 from retail_sales
 group by 1,2
 order by  1,3 desc;
 
 

-- Q.8 Write a SQL query to find the top 5 customers based on the highest total sales 

 select customer_id, sum (
total_sale ) as total_sales
 from retail_sales
 group by 1
order by 2 desc
limit 5;



-- Q.9 Write a SQL query to find the number of unique customers who purchased items from each category.


 select  category,
	  count ( distinct customer_id)
 from retail_sales
group by 1


 -- 10. Write a SQL query to calculate the total sales (total_sale) for each product category.

select category, 
   sum(total_sale) as total_sales
  FROM retail_sales
   group by 1
  order by  total_sales  DESC;

-- 11. Write a SQL query to find the average age of customers who purchased items from each category.

  
SELECT category, AVG(age) AS average_age
FROM retail_sales
GROUP BY category
ORDER BY average_age DESC;


-- 12. Write a SQL query to find the top 5 customers based on the highest total sales (total_sale).

select 
	customer_id,
	 sum(total_sale)  as total_sales
	from retail_sales
    group by customer_id
	order by total_sales desc
     limit 5;

 -- 13. Write a SQL query to calculate the total sales (total_sale) made by male and female customers.


    select gender ,
    sum (total_sale)   AS total_sales
    from retail_sales
     group by gender;
    

 -- 14.  Write a SQL query to calculate the total sales (total_sale) for each month of the year 2023.

 SELECT EXTRACT(MONTH FROM sale_date) AS month, SUM(total_sale) AS total_sales
FROM retail_sales
WHERE EXTRACT(YEAR FROM sale_date) = 2023
GROUP BY month
ORDER BY month;


-- 15. Write a SQL query to find the month with the highest total sales (total_sale) in the year 2023.



SELECT EXTRACT(MONTH FROM sale_date) AS month, SUM(total_sale) AS total_sales
FROM retail_sales
WHERE EXTRACT(YEAR FROM sale_date) = 2023
GROUP BY month
ORDER BY total_sales DESC
LIMIT 1;

-- 16.  Write a SQL query to calculate the total sales (total_sale) for each day.

 select sale_date ,
 sum (total_sale) AS total_sales 
	 from retail_sales
 group by sale_date
order by sale_date;

-- 17. Write a SQL query to find all transactions in the 'Electronics' category for 
-- 	customers between the ages of 30 and 40.


 select * from retail_sales
where category = 'Electronics' and age between 30 and 40;

-- 18. Write a SQL query to calculate the total sales (total_sale) for each gender in each product category.

   select  gender , category,
 sum (total_sale) as total_sales
	   from retail_sales
  group by gender, category
order by 3;


-- 19. Write a SQL query to find the transaction with the highest total_sale.


select * from  retail_sales
 order by  total_sale desc
 limit 1;



-- 20. Write a SQL query to find the total number of transactions made in each month of the year 2023.

select extract ( month from sale_date) as month , count (transactions_id) as total_transaction
 from retail_sales
 where  extract (year from sale_date) = 2023
 group  by month
 order by month;


-- END OF PROJECT--------
