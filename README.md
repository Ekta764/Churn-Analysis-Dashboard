📊 Churn Analysis Dashboard
A data analysis project combining SQL and Power BI to analyze customer churn patterns and identify at-risk customers for a telecom company.

🛠️ Skills Demonstrated

SQL (Microsoft Access) — Wrote queries to segment customers by risk, charges, contract type, and churn behavior
Power BI — Built a 4-page interactive dashboard with slicers, KPIs, charts, and custom visuals


📁 Project Structure
Churn-Analysis-Dashboard/
│
├── PowerBI/
│   └── Churn_Analysis_Dashboard.pbix
│
├── SQL/
│   └── churn_analysis.accdb
│   └── queries.sql
│
├── Screenshots/
│   └── overview.png
│   └── contract_analysis.png
│   └── payment_analysis.png
│   └── risk_analysis.png
│
└── README.md

SQL Queries
1. Churn by Internet Service
Calculates average monthly charges and total churned customers per internet service type.
sqlSELECT s.InternetService, AVG(s.MonthlyCharges) AS avg_monthly_charges, 
SUM(IIF(s.Churn = 'Yes', 1, 0)) AS churned
FROM Customers AS c INNER JOIN Services AS s ON c.customerID = s.customerID
GROUP BY s.InternetService;

2.  Early Churn Risk Customers
Identifies customers with tenure under 12 months on month-to-month contracts — highest churn risk segment.
sqlSELECT c.CustomerID, c.gender, c.Tenure, s.Contract
FROM Customers AS c INNER JOIN Services AS s ON c.CustomerID = s.CustomerID
WHERE c.Tenure < 12
AND s.Contract = 'Month-to-month';

3. High Risk Female Customers
Filters senior female customers on month-to-month contracts paying over $70/month.
sqlSELECT c.customerID, c.gender, s.Contract, s.MonthlyCharges, c.SeniorCitizen
FROM Customers AS c INNER JOIN Services AS s ON c.customerID = s.customerID
WHERE c.gender = 'Female'
AND c.SeniorCitizen = 1
AND s.Contract = 'Month-to-month'
AND s.MonthlyCharges > 70;

4. High Value Churned Customers
Finds churned customers paying over $70/month — highest revenue loss segment.
sqlSELECT c.customerID, c.tenure, s.Contract, s.MonthlyCharges, s.Churn
FROM Customers AS c INNER JOIN Services AS s ON c.customerID = s.customerID
WHERE s.Churn = 'Yes'
AND s.MonthlyCharges > 70
ORDER BY s.MonthlyCharges DESC;

5. Internet Service Breakdown
Counts total customers per internet service type.
sqlSELECT s.InternetService, COUNT(*) AS total_customers
FROM Customers AS c LEFT JOIN Services AS s ON c.customerID = s.customerID
GROUP BY s.InternetService
ORDER BY COUNT(*) DESC;

6. Phone Service Breakdown
Counts total customers by phone service subscription.
sqlSELECT s.PhoneService, COUNT(*) AS total_customers
FROM Customers AS c LEFT JOIN Services AS s ON c.customerID = s.customerID
GROUP BY s.PhoneService
ORDER BY COUNT(*) DESC;

7. Senior Citizens Who Churned
Identifies senior customers who have already churned.
sqlSELECT c.customerID, c.gender, c.SeniorCitizen, s.Churn
FROM customers AS c INNER JOIN services AS s ON c.customerID = s.customerID
WHERE c.SeniorCitizen = 1
AND s.churn = 'YES';

8. Average Charges by Gender
Compares average monthly charges and customer count between male and female customers.
sqlSELECT c.gender, AVG(s.MonthlyCharges) AS avg_monthly_charges, 
COUNT(*) AS total_customers
FROM Customers AS c INNER JOIN Services AS s ON c.customerID = s.customerID
GROUP BY c.gender
ORDER BY Count(*) DESC;

9. Churn by Contract Type
Summarizes churn, retention, and average tenure per contract type.
sqlSELECT s.Contract, COUNT(*) AS total_customers, 
SUM(IIF(s.Churn='Yes',1,0)) AS churned, 
SUM(IIF(s.Churn='No',1,0)) AS retained, 
AVG(c.tenure) AS avg_tenure_months
FROM Customers AS c INNER JOIN Services AS s ON c.customerID = s.customerID
GROUP BY s.Contract
ORDER BY SUM(IIF(s.Churn='Yes',1,0)) DESC;

10. Churn by Gender
Compares churn and retention rates between male and female customers.
sqlSELECT c.gender, COUNT(*) AS total_customers, 
SUM(IIF(s.Churn='Yes',1,0)) AS churned, 
SUM(IIF(s.Churn='No',1,0)) AS retained
FROM Customers AS c INNER JOIN Services AS s ON c.customerID = s.customerID
GROUP BY c.gender;

11. Full Customer Overview
Returns complete customer and service data joined across both tables.
sqlSELECT c.customerID, c.gender, c.tenure, s.Contract, s.MonthlyCharges, s.Churn
FROM Customers AS c INNER JOIN Services AS s ON c.customerID = s.customerID;

📊 Dashboard Pages
1. Overview

Total customers, churn rate, average monthly charges
High level KPIs and summary visuals

2. Contract Analysis

Churn breakdown by contract type
Retention rates across Month-to-month, One year, Two year contracts

3. Payment Analysis

Customers by payment method
Churn by payment method
Internet service breakdown by monthly charges

4. Risk Analysis

Early churn risk customers (1,908 identified)
High risk customer segments by gender and tenure
Gauge showing overall risk level
Tenure distribution of at-risk customers


📈 Key Insights

1,908 customers identified as early churn risk
Month-to-month contracts have the highest churn rate
Average monthly charge of at-risk customers: $64.76
Senior female customers on high monthly charges are highest risk segment
Customers with tenure under 12 months are most likely to churn


🗄️ Database Structure
Two main tables joined on customerID:
TableKey ColumnsCustomerscustomerID, gender, tenure, SeniorCitizenServicescustomerID, Contract, MonthlyCharges, Churn, InternetService, PhoneService

🚀 How to Use

Open churn_analysis.accdb in Microsoft Access to view SQL queries
Open Churn_Analysis_Dashboard.pbix in Power BI Desktop to explore the dashboard
Use slicers (InternetService, Contract, Gender) to filter all visuals


🏷️ Topics
power-bi sql microsoft-access data-analysis churn-analysis dashboard data-visualization
