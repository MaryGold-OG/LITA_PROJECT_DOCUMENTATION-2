# LITA_PROJECT_DOCUMENTATION-2

### Project Topic: Customer Subscription Analysis

[Project Overview](#project-overview) 

[Data Source](#data-source)

[Tools Used](#tools-used)

[Data Cleaning and Preparation](data-cleanimg-and-preparation)

[Exploratory Data Analysis](#exploratory-data-analysis)

[SQL-Based Queries](#sql-based-queries)

[Power BI Dashboard](#power-bi-dashboard)

[Data Analysis](#data-analysis)

[Data Visualization](#data-visualization)

[Key Insights](#key-insights)

[Recommendation](#recommendation)


### Project Overview
---
This project analyzes customer subscription data to understand key trends, identify popular subscription types, and observe regional distribution patterns. By examining metrics such as subscription durations, cancellation rates, and regional breakdowns, this analysis provides actionable insights into customer behavior and subscription performance. 

### Data Source 
---
The primary source of the Data used is from the Incubator Hub

### Tools Used 
---
- Microsoft Excel
    1. For Data cleaning
    2. For Analysis
    3. For Pivot Tables
- SQL - Structured Query Language for Querying of Data
- Power BI or Visualization
- Github for Portfolio Building

### Data Cleaning and Preparation
---
In the initial phase of the Data cleaning and preparations, I perform the following action;
    1. Data loading and Inspection
    2. Handling missing variables
    3. Data Cleaning and formating

### Exploratory Data Analysis (EDA)
---
- Analyzed regional distribution and identified the most popular subscription types.
- Calculated average subscription duration and identified trends in cancellations.

### SQL- Based Queries
---
- Retrieve the total number of customers from each region.
- Find the most popular subscription type by the number of customers. 
- Find customers who cancelled their subscription within 6 months. 
- Calculate the average subscription duration for all customers. 
- Find customers with subscriptions longer than 12 months. 
- Calculate total revenue by subscription type. 
- Find the top 3 regions by subscription cancellations. 
- Find the total number of active and cancelled subscriptions. 

### Power BI Dashboard:
---
- Visualized insights with metrics, cards, measures, and charts on key customer segments, cancellations, and subscription trends. Include slicers for interactive analysis.

### Data Analysis
---

This is where I include some basic Excel formulars, queries and some DAX functions used during the analysis;

```Excel Formulars
Subscription Duration =F2-E2
```
```Excel Formulars
Average Duration =AVERAGE(I:I)
```
```SQL
 Retrieve the total number of customers from each region----
Select Region, COUNT(CustomerID) Total_No_Of_Customers
from CustomerData
Group by Region
```
```SQL
Find the most popular subscription type by the number of customers---
Select Top 1 SubscriptionType, COUNT(CustomerID) As Total_No_Of_Customers
From CustomerData
Group By SubscriptionType
```
```SQL
Find customers who canceled their subscription within 6 months---
SELECT CustomerID, SubscriptionType, SubscriptionStart, SubscriptionEnd
FROM CustomerData
WHERE DATEDIFF(DAY, SubscriptionStart, SubscriptionEnd) <= 180;
```
```SQL
Calculate the average subscription duration for all customers
 Select AVG(Subscription_Duration) As Average_SubscriptionDuration 
 From CustomerData
```
```SQL
Find customers with subscriptions longer than 12 months
SELECT CustomerID, SubscriptionType, SubscriptionStart, SubscriptionEnd
FROM CustomerData
WHERE DATEDIFF(DAY, SubscriptionStart, SubscriptionEnd) > 365;
```
```SQL
Calculate total revenue by subscription type-----
Select SubscriptionType, SUM(Revenue) As TotalRevenue_SubscriptionType
From CustomerData
Group By SubscriptionType
```
```SQL
Find the top 3 regions by subscription cancellations----
SELECT TOP 3 Region, COUNT(Canceled) AS CancellationCount
FROM CustomerData
WHERE Canceled = 'True'
GROUP BY Region
ORDER BY CancellationCount DESC;
```
```SQL
Find the total number of active and canceled subscriptions----
SELECT 
    COUNT(CASE WHEN Canceled = 'False' THEN 'True' END) AS ActiveSubscriptions,
    COUNT(CASE WHEN Canceled = 'True' THEN 'False' END) AS CanceledSubscriptions
FROM CustomerData;
```
Measures Using DAX Function
```DAX
Total Revenue = SUM(CustomerData[Revenue])
```
```DAX
Active Subscriptions = COUNTROWS(FILTER(CustomerData, CustomerData[Canceled] = "False"))
```
```DAX
Canceled Subscriptions = COUNTROWS(FILTER(CustomerData, CustomerData[Canceled] = "True"))
```
```DAX
Average Subscription Duration = AVERAGE(CustomerData[Subscription Duration])
```
```DAX
Cancellation Rate = [Canceled Subscriptions] / ( [Active Subscriptions] + [Canceled Subscriptions] )
```

### Data Visualization
---

#### Excel workSheet
---
![Customer Data Excel Formular](https://github.com/user-attachments/assets/be7aa605-d949-4be9-bceb-28a0e79a6aeb)

#### Pivot Table
---
![Customer Data Pivot Table](https://github.com/user-attachments/assets/4821e73b-07a1-4d61-8e37-e51bd720cd4b)
---
#### SQL Queries
---
![Customer Query 1](https://github.com/user-attachments/assets/6d79c2bb-6511-4219-a7df-5fe120ccfc37)

![Customer Query 2](https://github.com/user-attachments/assets/a356423a-d624-4b1d-a2df-7e0eaf7dc442)

![Customer Query 3](https://github.com/user-attachments/assets/c74d1326-5ece-4fa0-a9f6-5994013b7f7c)

![Customer Query 4](https://github.com/user-attachments/assets/dde9730a-b21e-4551-a7e2-beaad63fdc31)

![Customer Query 5](https://github.com/user-attachments/assets/b6aed891-b1e5-4900-836a-8120ca6f0e8d)

![Customer Query 6](https://github.com/user-attachments/assets/e04cb9e8-499e-4400-94b1-e3b408bfd03f)

![Customer Query 7](https://github.com/user-attachments/assets/067d590b-9294-4c6d-afaf-9f4280482384)

![Customer Query 8](https://github.com/user-attachments/assets/440b128d-ded6-4306-a973-984d68facba8)

#### Power BI Dashboard
---
![Customer Data Dashboard 1](https://github.com/user-attachments/assets/6ce8addb-b517-4d5b-bdbe-84fe3df918d7)

![Customer Data Dashboard 2](https://github.com/user-attachments/assets/6eb8dce8-2398-4e8d-a017-a04b3f91d5e1)

### Key Insights
---
- Average Subscription Duration: The average subscription duration is approximately 365.35 days.
- Most Popular Subscription Type: The Basic subscription is the most popular, with the highest revenue of ₦33,776,735, followed by Premium (₦16,899,064) and Standard (₦16,864,376).
#### Yearly Revenue Trends:
- 2023 recorded the highest revenue at ₦40,538,438, while 2024 had a lower revenue of ₦27,001,737. This indicates a significant cancellation rate in 2023.
- Regional Revenue Comparison:
- Revenue generated by each region (East, North, South, and West) shows minimal variation, with differences of 1-2%.

#### Subscriber Decline 
- The number of subscribers declined by 44.91% in 2023, suggesting a notable drop in retention.

#### Cancellation Rates by Subscription Type
- Basic: 5,067
- Premium: 5,064
- Standard: 5,044
- There is only a slight difference in cancellation rates across subscription types.

#### Monthly Trends:
- April saw the highest number of canceled subscriptions.
- July recorded the highest number of active subscribers.


### Recommendation
---

- Since the Basic subscription is the most popular, enhancing its value to retain and attract even more customers should be considered. This could include offering additional benefits, loyalty rewards, or optional add-ons to increase customer satisfaction and revenue.

- With 2023 showing high cancellation rates and a significant decline in subscribers (44.91%), it’s critical to investigate the root causes. Customer feedback surveys should be conducted, consider implementing a retention program, such as discounts or special promotions, to improve customer retention.

- With an average subscription duration of 365.35 days, longer-term subscriptions to boost revenue stability should be encouraged.

- Since Basic subscriptions significantly outperform Standard and Premium in both popularity and revenue, I will recommend reviewing the pricing and benefits of the Premium and Standard plans. Adjusting these plans to enhance their appeal could drive interest and balance subscription revenue distribution across all types.
