# DSA-Project-Case-Study-2-Femi-Abugo
DSA Project Case Study 2 is for Case Study 2: Kultra Mega Stores Inventory.

The company overview : Kultra Mega Stores (KMS), headquartered in Lagos, specialises in office supplies and
furniture. Its customer base includes individual consumers, small businesses (retail), and
large corporate clients (wholesale) across Lagos, Nigeria.
I am engaged as a Business Intelligence Analyst to support the Abuja division of
KMS. The Business Manager shared an Excel file containing order data from 2009 to
2012 and requested that I analyze the data and present mh key insights and
findings, thereby presenting two scenarios to the case study.

# PROJECT STEPS
Applying my SQL skills from the DSA Data Analysis class, tasks were actioned to solve both case scenarios
as shared in the document. 
1. Using SQL Server Managemeng studio, a database was created and data provided imported as a table into the database.
2. Data was cleaned and data type was optimised in the process.
   * Sales, Profit, Discount, Shipping_Cost changed to DECIMAL(10,2)
   * Quantity, Order_ID, Product Count changed to INT
4. The business questions were analysed to assist in providing management decisions and insights generated from the SQL queries written to ptovide amswers go ghe business questions.

# CASE SCENARIO 1 (Business Questions & Insights)
select *
from [KMS Sql Case Study]

1. Which product category had the highest sales? OFFICE SUPPLIES WITH 4610 SALES
select top 1 [Product_Category],count ([Product_Category])as [Product Count]
from [KMS Sql Case Study]
group by Product_Category
order by [Product Count] desc
   
2. What are the Top 3 and Bottom 3 regions in terms of sales?
TOP 3
select top 3 [Region],sum([sales]) as [Total Sales]
from [KMS Sql Case Study]
group by Region
order by [Total Sales] desc

BOTTOM 3
select top 3 [Region],sum([sales]) as [Total Sales]
from [KMS Sql Case Study]
group by Region
order by [Total Sales] asc

3. What were the total sales of appliances in Ontario?

select Region, SUM(sales) as [Total Sales]
from [KMS Sql Case Study]
where Region='ontario'
Group by Region

4. Advise the management of KMS on what to do to increase the revenue from the bottom
10 customers

Select top 10 [Customer_Name], SUM([Sales]) as [Total Sales]
from [KMS Sql Case Study]
group by Customer_Name
order by [Total Sales] desc

ADVICE
* Improve customer engagement to identify the requirements for their terrain
* Carry out promos and give more discounts to increase turnover

5. KMS incurred the most shipping cost using which shipping method?

Select Top 1 [Ship_Mode], SUM([Shipping_Cost]) as [Total Shipping Cost]
from [KMS Sql Case Study]
group by Ship_Mode
order by [Total Shipping Cost] desc



# CASE SCENARIO 2 (Business Questions & Insights)
6. Who are the most valuable customers, and what products or services do they typically
purchase?

select [Customer_Name],Product_Name, SUM(sales) as [Total Sales]
from [KMS Sql Case Study]
Group by Customer_Name,Product_Name
order by [Total Sales] desc


7. Which small business customer had the highest sales?

select top 1 Customer_Name,Customer_Segment, SUM([Sales]) as [Total Sales]
from [KMS Sql Case Study]
where Customer_Segment ='small Business'
group by Customer_Name,Customer_Segment
order by [Total Sales] desc

   
8. Which Corporate Customer placed the most number of orders in 2009 – 2012?

select top 1  Customer_Name,Customer_Segment, count([Order_ID]) as [Total order]
from [KMS Sql Case Study]
where Customer_Segment ='corporate' and Order_Date between '2009' and '2012'
group by Customer_Name,Customer_Segment
order by [Total order] desc


9. Which consumer customer was the most profitable one?

select top 1 Customer_Name,Customer_Segment, sum([Profit]) as [Total profit]
from [KMS Sql Case Study]
where Customer_Segment ='Consumer'
group by Customer_Name,Customer_Segment
order by [Total profit] desc


10. Which customer returned items, and what segment do they belong to?

select Customer_Name,Customer_Segment,[Status]
from [KMS Sql Case Study]
join [dbo].[Order_Status]
on [KMS Sql Case Study].Order_ID = [dbo].[Order_Status].[Order_ID]


11. If the delivery truck is the most economical but the slowest shipping method and
Express Air is the fastest but the most expensive one, do you think the company
appropriately spent shipping costs based on the Order Priority? Explain your answer

Select Order_Priority, Ship_Mode,
    COUNT([Order_ID]) AS [order count],
    SUM(sales - profit) AS [Estimated shipping cost],
    AVG(DATEDIFF(DAY, [Order_Date], [Ship_Date])) AS [Avg ship date]
from  [KMS Sql Case Study] 
group by Order_Priority,Ship_Mode
order by  Order_Priority,Ship_Mode desc 

No, from the data gathered the company did not appropriately spend shipping costs based on the Order Priority.

