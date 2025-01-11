# S-Mart-Sales-Analysis
This project analyzes S-Mart sales data using SQL, focusing on sales trends, product performance, and customer behavior across Beauty, Clothing, and Electronics categories.

# Write a SQL query to retrieve all columns for sales made on '2022-11-05

SELECT * FROM sales_retail
WHERE sale_date = '2022-11-05';


# Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4 in the month of Nov-2022
select *
From sales_retail
Where category = 'Clothing'
and quantiy > 4 and
CHAR (sale_date, yyyy-mm) = '2020-11';


# Write a SQL query to calculate the total sales (total_sale) for each category.
select category, Sum(total_sale) from sales_retail
group by category;


# Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.

Select category, Round(avg(Age), 2) As Average_Age From sales_retail
where category = 'Beauty';


# Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.
Select Count(transactions_id), gender, category From sales_retail
group by category, gender;


# Write a SQL query to find all transactions where the total_sale is greater than 1000.

Select * from sales_retail
where total_sale > 1000;



# Write a SQL query to calculate the average sale for each month. Find out best selling month in each year

select
Round(avg(total_sale),2) as AVG_Total,
year(sale_date) as 'Years',
Month(sale_date) as 'Months'
from
sales_retail
group by year(sale_date), Month(sale_date)
order by AVG_Total desc
Limit 5;


# Write a SQL query to find the top 5 customers based on the highest total sales.

Select customer_id , sum(Total_sale) From sales_retail
Group By customer_id
Order by Sum(total_sale) desc
Limit 5;


# Write a SQL Query to find the number of unique customers who purchased items from each category.

select
Count(distinct(customer_id)) as 'Unique Customers for each Category',
category
from
sales_retail
group by category;


# Write a SQL query to create each shift and number of orders (Example Morning <12, Afternoon Between 12 & 17, Evening >17)

select Count(customer_id) as Total_Order,
case
when Hour(sale_time) < 12 then 'Morning'
When Hour(sale_time) between 12 and 17 then 'Afternoon'
else 'Evening'
End as 'Shift'
from sales_retail
Group by Shift;

Select count(customer_id) ,
case
when extract(hour from sale_time) < 12 then 'Morning'
when extract(Hour from sale_time) between 12 and 17 then 'Afternoom'
Else 'Evening'
End as Shifts
From sales_retail
Group by Shifts;
