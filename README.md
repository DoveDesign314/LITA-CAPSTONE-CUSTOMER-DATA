# Customer Segmentation and Retention Analysis for Subscription Services
---
## Project Outline
---
[Project Overview](#project-overview)

[Project Workflow](#project-workflow)

[Data Source](#data-source)

[Datasets and column definitions](datasets-and-column-definitions)

[Key Insights from the Data](#key-insights-from-the-data)

[Tools Used](#tools-used)

[Data Cleaning and Preparation (Excel)](#data-cleaning-and-preparation)

[Key steps](#key-steps)

[Formula Used](#formula-used)

[Exploratory Data Analysis](#exploratory-data-analysis)

[Data Analysis (SQL)](#data-analysis-(sql))

[Data Visualization (Power BI)](#data-visualization-(power-bi))

[Key Findings](#key-findings)


### Project Overview
---
This project aims to analyzes customer data in identifying key segments and behavioral trends within a subscription service. The objective is to explore customer behavior patterns, track different subscription types, and detect critical trends in cancellations and renewals. The deliverable is a Power BI dashboard that visualizes these insights, providing a comprehensive view of customer retention and segment-based performance.

### Project Workflow 
---
The project was completed in three phases: data cleaning and exploration in Excel, query-based analysis using SQL, and final visualization in Power BI. 

### Data Source 
---

The primary source of data used here was Customer Data.xlsx 

### Datasets and column definitions 
---

The Customer data used in this project consists of multiple columns that capture key information about sales transactions. Below is an explanation of each column in the dataset: 

• CustomerId: A unique identifier assigned to each customer in the dataset, such as 201, 202 etc.

• Customer Name: The full name of the customer associated with the subscription, such as John, Jane, Alex etc.

• Region: The geographical location or area where the customer resides or where the subscription is active, such as North, South, East and West.

• Subscription Type: The category or level of subscription chosen by the customer (e.g., Basic, Premium and Standard). 

• Subscription Start: The date when the customer's subscription began. 

• Subscription End: The date when the customer's subscription is set to end or renew.

- Canceled: Indicates whether the subscription was canceled, typically as a "Yes" or "No" value.

- Revenue: The total revenue generated from the customer’s subscription.

### Key Insights from the Data 

---
Here are some of the key insights derived from the customer subscription data:

1. Top-Performing Regions: Identify which regions generate the highest revenue and have the most active subscriptions, helping target marketing and retention efforts more effectively.

2. Popular Subscription Types: Analyze the distribution of subscription types (e.g., Basic, Premium) to understand customer preferences and identify high-value segments.

3. Revenue Trends: Track monthly revenue trends, highlighting periods with increased revenue or higher cancellations for possible seasonal patterns.

4. Subscription Lifecycle Analysis: Determine the average subscription duration across types, offering insight into how long customers typically remain subscribed before canceling or renewing.

5. Behavioral Patterns in Cancellations: Investigate patterns in cancellations, such as whether they occur more often with specific subscription types, in certain regions, or after a certain duration.

6. Revenue per Customer Segment: Segment customers by subscription type or region to determine which segments are the most profitable, guiding targeted strategies to increase revenue from high-value customers.


### Tools Used 
---
1.  Microsoft Excel [Download Here](https://www.microsoft.com/en-us/microsoft-365/excel)

• For initial data cleaning, 

• For analysis, 

• For exploration and 

• For Data visualization. 

2. Microsoft SQL Server [Download Here](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
   - Other SQL database you can use include MySQL: [Download MySQL](https://dev.mysql.com/downloads/), PostgreSQL: [Download PostgreSQL](https://www.postgresql.org/download/)

• For data extraction 

• For advanced querying from the sales database. 

3.  Power BI [Downloaad Here](https://powerbi.microsoft.com/en-us/downloads/)

• For data visualization 

• For dashboard creation. 

4  Github for portfolio Building [Download Here](https://github.com/)
- From this page, you can sign up, create repositories, and explore open-source projects.


### 1. Data Cleaning and Preparation (Excel) 
---

The sales data was first explored and cleaned in Excel. The following actions were done: 

• Data loading and Inspection. 

• Handling missing variables, removing duplicates and formatting columns. 

• Data validation to ensure consistency  

• Basic exploratory analysis, such as Subscription Duration, Most popular subscription type, total revenue etc using pivot tables. 

Key Steps: 

• Filtered sales data for the analysis period. 

• Created summary/pivot tables for subscription type categories, regions, and sales channels. 

• Calculated key metrics such as average subscription duration and total revenue by subscription type. 

### Formula Used 
---

• Subscription Duration 
```Excel
=DATEDIF([Subscription Start], [Subscription End], "M")  // for months
```
or 
```Excel
==F2 - E2
```
F2 - Subscription End, E2 - Subscription Start


### Exploratory Data Analysis 
---
The structured approach to perform Exploratory Data Analysis (EDA) on the customer subscription data in Excel include 
1. Descriptive Statistics -Revenue Totals and Averages, Count and Frequency etc
2. Trend Analysis - Revenue Over Time
3. Segmentation Analysis -Use Pivot Tables to group by Subscription Type and calculate metrics like total revenue, average revenue per type. This helps understand which subscription types are most valuable.

EDA was used to explore and to answer some questions about the Data such as; 

• what is the total and average revenue per customer and per subscription type? 

• which subscription types are most popular? 

• which subscription types generate the most revenue?


### 2. Data Analysis (SQL) 
---

After the initial data preparation, SQL was used to run more advanced queries on the dataset , allowing deeper insights. 

Key SQL Queries: 

• To find the top 3 regions by subscription cancellations
```SQL
SELECT  Top (3) Region, COUNT(CustomerID) AS Cancellations
FROM [dbo].[Customer Data]  WHERE Canceled = 'TRUE'
GROUP BY Region
ORDER BY Cancellations DESC;
```

• To calculate total revenue by subscription type
```SQL
SELECT [SubscriptionType], SUM(CAST(REPLACE(LTRIM(RTRIM([Revenue])), ',', '') AS DECIMAL(10, 2))) AS TotalRevenue
FROM [dbo].[Customer Data]
GROUP BY [SubscriptionType]
ORDER BY TotalRevenue DESC
``` 

• To retrieve the total number of customers from each region
```SQL
SELECT [Region], COUNT([CustomerID]) AS TotalCustomers
FROM [dbo].[Customer Data]
GROUP BY [Region];
```

• To find the most popular subscription type by the number of customers
```SQL
SELECT [SubscriptionType], COUNT([CustomerID]) AS MostPopularSubscriptionType
FROM [dbo].[Customer Data]
GROUP BY [SubscriptionType]
ORDER BY MostPopularSubscriptionType DESC
```

• To calculate the average subscription duration for all customers
```SQL
SELECT AVG(DATEDIFF(day, [SubscriptionStart], [SubscriptionEnd])) 
AS AverageSubscriptionDurationDays
FROM [dbo].[Customer Data];
```

### 3. Data Visualization (Power BI) 
---

DAX Measures for key insights were created: 

• Total Sales: 

TotalSales = SUMX(Sales, Sales[Quantity] * Sales[UnitPrice]) 

• Sales by Region 

SalesByRegion = SUM(Sales[TotalSales]) 

The final stage was to visualize the insights using Power BI. The interactive dashboard includes: 

• Top-Performing Products: A bar chart showing the products that brought in the highest revenue. 

Axis: Product Name. Values: Total Sales (using TopProductSales). 

• Regional Sales Performance: A map chart displaying total sales by region. 

Location: Region Values: Total Sales 

• Monthly Sales Trends: A line chart visualizing sales trends over time. 

X-axis: Order Date Y-axis: Total Sales. 

Key Findings 

• Top-Selling Products: The top 3 products accounted for 40% of total sales, with Product A leading the list. 

• Regional Performance: Region X generated the highest sales, contributing to 35% of the overall revenue. 

• Sales Trends: The highest sales occurred in December, with a steady increase observed in the 
