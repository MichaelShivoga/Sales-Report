
--Pizza Database Project

Select *
From pizza_sales

--Total Revenue
--This is the Sum of the Total_price

Select Cast(SUM(total_price) AS decimal(10,2)) as Total_revenue
From pizza_sales

--AVG Order value
--AVG Amount spent per Order

Select SUM(total_price)/ COUNT(distinct order_id) as Avg_order_value
From pizza_sales

--Total Pizza Sold

 Select SUM(quantity) as Total_pizzaz_sold
 From pizza_sales

 --Total Orders

 Select Count(distinct order_id) as total_order
 From pizza_sales

 --AVG Pizza per order

 Select CAST(SUM(quantity) / COUNT(distinct order_id) As decimal(10,2)) as avg_pizza_per_order
 From pizza_sales



 --SALES TRENDS
--Daily Trends

 Select DATENAME(DW, order_date) as order_day, COUNT(distinct(order_id)) as total_order
 From pizza_sales
 Group By DATENAME(DW, order_date) 

 --Month Trend of Total Sales

 Select DATENAME(MONTH, order_date) as Month_name, Count(distinct(order_id)) as Total_sales
 From pizza_sales
 Group by DATENAME(MONTH, order_date)
 Order by Total_sales Desc 

 --Percentage of Sales by Pizza Category

 Select pizza_category, CAST(Sum(total_price)*100 / (Select SUM(total_price) From pizza_sales) AS DECIMAL(10,2)) as Sales_percentage_by_category
 From pizza_sales
 Group By pizza_category
 Order By Sales_percentage_by_category Desc


 --Percentage of Sales By Pizza Size

 Select pizza_size, CAST(SUM(total_price)*100 / (Select SUM(total_price) From pizza_sales) AS decimal(10,2)) as sales_percentage_by_size
 From pizza_sales
 Group by pizza_size
 Order By sales_percentage_by_size Desc

 --Total Pizza Sold By Group Category

 Select pizza_category, SUM(quantity) as pizza_sales_by_category
 From pizza_sales
 Group By pizza_category
 order by pizza_sales_by_category Desc

 --Top 5 pizza by revenue

 Select Top 5 pizza_name, SUM(total_price)AS total_sales
 From pizza_sales
 Group by pizza_name
 Order by total_sales Desc

--Botton 5 Pizza by Revenue

Select Top 5 pizza_name, SUM(total_price) as total_sales
From pizza_sales
Group by pizza_name
order by total_sales ASC

--Top 5 pizza by Quantity

Select Top 5 pizza_name, SUM(quantity) as total_quantity
From pizza_sales
Group By pizza_name
Order by total_quantity Desc

--Bottom 5 pizza by quantity

Select Top 5 pizza_name, SUM(quantity) as total_quantity
From pizza_sales
Group By pizza_name
Order by total_quantity ASC
 
--Top 5 Pizza by total orders

Select Top 5 pizza_name, Count(distinct(order_id)) as total_orders
From pizza_sales
Group by pizza_name
Order By total_orders Desc

--Bottom 5 Pizza by Total Orders

Select Top 5 pizza_name, Count(distinct(order_id)) as total_orders
From pizza_sales
Group by pizza_name
Order By total_orders ASC

