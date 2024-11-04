# Customer Subscription and Trends Data Analysis

##Table of contents
- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Analysis Tools](#analysis-tools)
- [Data Cleaning](#data-cleaning)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results](#results)
- [Recommendations](#recommendations)
- [Limitations](#limitations)


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


### Data Cleaning
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
1. Targeted Retention Strategies for High-Cancellation Regions
The East, South, and North regions have the highest cancellation rates. Focus on understanding the specific challenges or dissatisfaction in these regions through customer feedback surveys and targeted engagement. Consider region-specific offers, personalized communication, or loyalty programs to improve customer retention.Enhance Subscription Offerings

2. Since the Basic subscription is the most popular and highest revenue generator, there might be an opportunity to enhance its value. Introduce add-ons or upsell features to encourage upgrades to Premium or Standard subscriptions. Also, analyze why the Standard subscription is less favored and re-evaluate its pricing or feature set.Improve Subscription Duration Beyond 12 Months

3. Currently, no customers have a subscription duration beyond 12 months. To increase long-term commitment, consider offering incentives like discounts, exclusive content, or bonus features for customers who commit to longer-term subscriptions (e.g., 18 or 24 months).Address Early Cancellations

4. With 15,175 customers ending their subscription within six months, it is critical to address early churn. Implement an onboarding process that highlights the value of the subscription, personalized customer support, and early check-ins to resolve issues promptly. Offering satisfaction guarantees or flexible subscription options could also reduce early cancellations.Regional Growth Opportunities

5. The East and South regions have the highest customer counts but also the highest cancellations. Focus on retention strategies while exploring growth opportunities in the West, which has the lowest customer base. Tailored marketing campaigns and region-specific promotions could help boost customer acquisition in underrepresented areas.

### Limitations
I had to remove duplicates from each column and row as that would affect the accuracy of my analysis result.








