# ETL-Sales_Analysis_Report---MySQL-PowerBI,
# To view the Responsive Power BI dashboard click here : https://app.powerbi.com/groups/me/reports/fb8e7d0e-71c7-4786-a8aa-645aff74b836/ReportSection

## Description of the scenerio? PROBLEM STATEMENT!
* Let's say a company is facing isuues with thier Sales and as a Data Analyst or Data Scientist what insights can you pull out from the Sales data?

* Firstly, you got to design a Strategy to tackle the problem. Usually Project Manager's use something called as AIMS Grid to project plan who all will be involved or bascially find out the relations to sort this issue for the company. https://www.coverdale.de/fileadmin/Germany/Toolbox/Aims-grid.pdf

## A Picture is worth more than a thousand words, right?
* Hence, we will execute ETL(Extract,Transform,Load) on MySQL and create a responsive dashboard in PowerBi and finally understand the business opportunities, patterns and   trends within data via visualization graphs! This can be the Solution to the uplift the Companies Sales. Data Never Lies!!!

## Let's Go!

### Dependencies

* Basic Knowledge about SQL and Microsoft Power BI tools.

## Steps :

### Extract
* Create an SQL database in SSMS(MySQL Workbench) and load/extract the data from MySql Database. 
# NOte: 
* Usually in companies they create a "Data Warehouse" using ETL and from there follow with,
*  Data Modelling - Data Cleaning - Data Transformation - Data Visualization and so on.

![alt text](https://www.altexsoft.com/media/2021/03/the-etl-workflow.png)

## Data Model,
* Create a simple dataflow in PowerBI Model. (You can also do it on VSCODE using SSIS integration).

* Here, I''m following a Star Schema to Model,
* You can Learn more about Data Modelling if you follow this free course, https://www.sqlbi.com/p/introduction-to-data-modeling-for-power-bi-video-course/

![alt text](https://github.com/immanuvelprathap/ETL-Sales_Analysis_Report---MySQL-PowerBI/blob/main/Data%20Model%20-%20Relationship.png)

* Now, apply necessary Transformations, (Very Similar to Data Preprocessing Steps in ML),

## I have used these SQL formulas/Syntax, 

### To know more on SQL Syntax : https://www.w3schools.com/sql/sql_syntax.asp

1. To show all customer records

    `SELECT * FROM customers;`

1. To show total number of customers

    `SELECT count(*) FROM customers;`

1. To show transactions for Chennai market (market code for chennai is Mark001

    `SELECT * FROM transactions where market_code='Mark001';`

1. To show distrinct product codes that were sold in chennai

    `SELECT distinct product_code FROM transactions where market_code='Mark001';`

1. To show transactions where currency is US dollars

    `SELECT * from transactions where currency="USD"`

1. To show transactions in 2020 join by date table

    `SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;`

1. To show total revenue in year 2020,

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.currency="INR\r" or transactions.currency="USD\r";`
	
1. To show total revenue in year 2020, January Month,

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and and date.month_name="January" and (transactions.currency="INR\r" or transactions.currency="USD\r");`

1. To show total revenue in year 2020 in Chennai

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020
and transactions.market_code="Mark001";`


Formulas used in Power BI,
============================

1. Formula to create norm_amount column

`= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)`

1. Formula for Revenue

`Revenue = SUM('Sales transactions'[norm_sales_amount])`
 
 1. Formula for Revenue Contribution percentage,
 
 `Revenue Contribution % = DIVIDE([Revenue],CALCULATE([Revenue],ALL('sales products'),ALL('sales customers'),ALL('sales markets')))`

## Key Insights,
![alt text](https://github.com/immanuvelprathap/ETL-Sales_Analysis_Report---MySQL-PowerBI/blob/main/sales_insights_report_page-0001.jpg)

## Profit Analysis,
![alt text](https://github.com/immanuvelprathap/ETL-Sales_Analysis_Report---MySQL-PowerBI/blob/main/sales_insights_report_page-0002.jpg)

## Performance Analysis,
![alt text](https://github.com/immanuvelprathap/ETL-Sales_Analysis_Report---MySQL-PowerBI/blob/main/sales_insights_report_page-0003.jpg)
