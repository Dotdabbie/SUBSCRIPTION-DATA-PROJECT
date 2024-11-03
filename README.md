# Customer Subscription and Trends Data Analysis



### Project Overview
This project analyzes subscription data to uncover customer behavior and key trends in cancellations and renewals using Excel, SQL, and Power BI.

**Excel Analysis:** Using Excel pivot tables, I explored subscription patterns, calculated average subscription durations, and identified popular subscription types. This allowed for quick insights and data validation before in-depth SQL analysis.

**SQL Queries:** I loaded the data into SQL Server to gain further insights. SQL queries were crafted to calculate metrics like average subscription duration, regional customer distribution, popular subscription types, total revenue by type, and cancellation trends. This provided a strong foundation for visual analysis.

**Power BI Dashboard:** The final deliverable was an interactive Power BI dashboard, designed to visualize customer segments, trends in subscription cancellations, and subscription duration. Key performance indicators (KPI cards) highlighted essential metrics like total active and canceled subscriptions, top regions for cancellations, and revenue by subscription type. Interactive slicers enabled dynamic filtering by region, subscription type, and status, adding flexibility for stakeholder-driven analysis.


### Data Source
The primary dataset used for this analysis is the "LITA Capstone Dataset_XLSX". it contained informations as:
1. CustomerID
2. Customer Name
3. Region
4. Subscription Type
5. Subscription start
6. Subscription end
7. Cancelled
8. Revenue


### Analysis Tools
-**Excel Analysis:** 

-[download here](https://microsoft.com)

I cleaned the data by removing duplicate data using Excel remove duplicate option. Using Excel pivot tables, I explored subscription patterns, calculated average subscription durations, and identified popular subscription types. This allowed for quick insights and data validation before in-depth SQL analysis.

-**SQL Queries:** 

-[download here](https://microsoft.com)

I loaded the data into SQL Server to gain further insights. SQL queries were crafted to calculate metrics like average subscription duration, regional customer distribution, popular subscription types, total revenue by type, and cancellation trends. This provided a strong foundation for visual analysis.

-**Power BI Dashboard:** 

-[download here](https://microsoft.com)

The final deliverable was an interactive Power BI dashboard, designed to visualize customer segments, trends in subscription cancellations, and subscription duration. Key performance indicators (KPI cards) highlighted essential metrics like total active and canceled subscriptions, top regions for cancellations, and revenue by subscription type. Interactive slicers enabled dynamic filtering by region, subscription type, and subscription status(active/renewals or cancelled), adding flexibility for stakeholder-driven analysis.


### Data Cleaning/Preparation process
This was done through the following:
- Data loading
- Data inspecction
- Removal of data duplicates
- Data formatting


### Exploratory Data Analysis
The data analysis is to answer key questions as;

- Analysing customer data to understand customer behaviour
- track subscription types
- identify key trends in cancellations and renewals.

### Data Analysis

```Excel for subscription duration in days
=DAYS(F2,E2)
```


```SQL
select region,
COUNT(customerID) as 
total_customers
from [dbo].[subc_data pro]
group by region;
```


```sql
select subscriptiontype,
count (customerid) as
total_customers
from [dbo].[subc_data pro]
group by subscriptiontype
order by total_customers desc
```


```sql
select customerid,
customername
from [dbo].[subc_data pro]
where subscriptionend is not null
and datediff(month,subscriptionstart,subscriptionend)<= 180
and canceled = 1;

```

```sql
select AVG(datediff(MONTH,subscriptionstart,ISNULL(subscriptionend, getdate()))) 
as AvgDuration
from [dbo].[subc_data pro]

```

```sql
SELECT CUSTOMERNAME
FROM [dbo].[subc_data pro]
WHERE DATEDIFF(MONTH,SUBSCRIPTIONSTART, 
ISNULL (SUBSCRIPTIONEND,GETDATE()))>12;

```

```sql
SELECT SUBSCRIPTIONTYPE,
SUM(REVENUE) AS
TOTAL_REVENUE
FROM [dbo].[subc_data pro]
GROUP BY SUBSCRIPTIONTYPE;

```

```sql
SELECT TOP 3 REGION, COUNT(*)AS CANCELLATIONS 
FROM [dbo].[subc_data pro]
WHERE SUBSCRIPTIONEND IS NOT NULL
GROUP BY REGION
ORDER BY CANCELLATIONS DESC

```

```sql
SELECT SUM(CASE WHEN
SUBSCRIPTIONEND IS NULL
THEN 1 ELSE 0 END) AS ACTIVESUBSCRIPTIONS,
SUM(CASE WHEN
SUBSCRIPTIONEND IS NOT NULL THEN 1 ELSE 0 END) AS
CANCELEDSUBSCRIPTIONS
FROM [dbo].[subc_data pro]

```

### Results:
1. The top 3 regions with the highest cancellations are arranged in decending orders;

    -East

   -South

   -North
3. The subscription duration is 365 days(12 months). There was no customer with a subcription above this duration.
4. The total revenue by subscription type in decending order;

    -Basic

   -Premium

   -Standard
6. most popular subscriptiontype based on customer count in descending order;

    -basic

   -premium

   -standard
8. 15,175 customers ended thier subscription before 6 months
9. The total number of customer per region in descending order;
   - East
   - south
   - north
   - west

### Recommendations









