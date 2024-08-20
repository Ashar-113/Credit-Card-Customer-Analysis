# Credit Card Customer Analysis
## Project Summary
This project is a Power BI report giving an in-depth analysis of the customers owning credit cards. It emphasises on the multiple metrics for the stakeholders of the credit card company. The report shows that the company has a revenue generation of a staggering $55.32 million while the revolving balance is $12 million. The company has earned $8 million as interest from the customers while the customer satisfaction score is 3.19 out of 5. Furthermore, the report covers revenue by quarter, customer expenditure preference, type of jobs they do, if they took loans, customer's income group, revenue from card category, etc. Further breakdown of the report and insights are discussed in this report below.
## Data Preparation and Modelling
The dataset is available in CSV format with two tables one containing data about the customer and the other table about their card details. The data was imported to the SQL server using MS SQL Management Studio. The intent to do so is the replication of real-world applications where data is updated in the databases and the report can be refreshed accordingly to keep the stakeholders updated with the changes in the data. The data was imported into the SQL database using the following queries:
The query below is used to create a database in SQL
```
CREATE DATABASE CC_db;
```
Next is to create the table for card details
```
CREATE TABLE cc_detail (
    Client_Num INT,
    Card_Category VARCHAR(20),
    Annual_Fees INT,
    Activation_30_Days INT,
    Customer_Acq_Cost INT,
    Week_Start_Date DATE,
    Week_Num VARCHAR(20),
    Qtr VARCHAR(10),
    current_year INT,
    Credit_Limit DECIMAL(10,2),
    Total_Revolving_Bal INT,
    Total_Trans_Amt INT,
    Total_Trans_Ct INT,
    Avg_Utilization_Ratio DECIMAL(10,3),
    Use_Chip VARCHAR(10),
    Exp_Type VARCHAR(50),
    Interest_Earned DECIMAL(10,3),
    Delinquent_Acc VARCHAR(5)
);
```
Following the card details we have a table for customer details
```
CREATE TABLE cust_detail (
    Client_Num INT,
    Customer_Age INT,
    Gender VARCHAR(5),
    Dependent_Count INT,
    Education_Level VARCHAR(50),
    Marital_Status VARCHAR(20),
    State_cd VARCHAR(50),
    Zipcode VARCHAR(20),
    Car_Owner VARCHAR(5),
    House_Owner VARCHAR(5),
    Personal_Loan VARCHAR(5),
    Contact VARCHAR(50),
    Customer_Job VARCHAR(50),
    Income INT,
    Cust_Satisfaction_Score INT
);
```
The data can be seen in the SQL database as follows after copying it from CSV files
#
![db detail](https://github.com/user-attachments/assets/b422fc72-873c-4c41-a911-d64fdd71c2e7)
![db customer](https://github.com/user-attachments/assets/e6889ca2-203b-456d-91ee-fb15381a3210)
### Data Modelling
The model consists of both tables imported into Power BI from the SQL database. Both are linked together with *Client_Num* columns in the respective tables so that insights can be produced in a meaningful manner. This table is shown below:
#
![model](https://github.com/user-attachments/assets/f117e3d3-466e-4c75-bc5d-6dd56ba98c8c)
### Measure Table
Keeping your work neat and structured can be achieved proactively with a measure table. All of the DAX expressions needed to assess the dashboard's KPIs are included in the measure table for the analysis. The dashboard analysis employs the following DAX expressions:
**Total Interest Earned:** One of the KPIs is used by writing the following DAX expression:
```
Total Interest Earned = SUM(credit_card_detail[Interest_Earned])
```
**Current Week Revenue:** To calculate the revenue generated for the ongoing week.
```
Current_week_Reveneue = CALCULATE(
SUM('credit_card_detail'[Revenue]),
FILTER(
ALL('credit_card_detail'),
'credit_card_detail'[Week no.] = MAX('credit_card_detail'[Week no.])))
```
**Previous Week Revenue:** To calculate the previous week's revenue to compare the difference between the two weeks for an entire year.
```
Previous_week_Reveneue = CALCULATE(
SUM('credit_card_detail'[Revenue]),
FILTER(
ALL('credit_card_detail'),
credit_card_detail[Week no.] = MAX(credit_card_detail[Week no.])-1))
```
## Project Overview
The report further gives deep insights into the financial conditions of the customer. This gives an idea of why customers might be delaying their payments or not being able to pay back what they owe. It can be observed that customers are spending their credit mostly on bills and entertainment. The report indicates that most customers are self-employed while retirees use the least amount of credit. Also, most customers belong to the low-income group while having two to three people depending on them in most cases. The significant amount of revenue generation was from the *Blue* category of the credit card. It is noteworthy that only 6% of the customers failed to pay back their credit.
#
![dash](https://github.com/user-attachments/assets/39244454-184d-4756-9df9-d5bcb53ff599)
![dash1](https://github.com/user-attachments/assets/2b58591f-e8de-4ca4-9894-38f6852f385f)
