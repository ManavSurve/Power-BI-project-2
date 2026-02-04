
## Data Source:MYSQL Datasource and SQL Server

### Dashboard Link : https://app.powerbi.com/groups/me/reports/384d017e-e935-44dc-9e7d-1626c1a36de1/ReportSection

## Problem Statement
1. The Business Context
​Modern businesses often operate with fragmented data stored across multiple relational database systems (e.g., MySQL for transactional web data and SQL Server for internal ERP/Financial records). This "data silo" effect prevents leadership from seeing the direct correlation between supply chain bottlenecks and financial losses.
​2. The Core Problem
​The organization currently lacks a unified view of its operational health. Specifically, there is an inability to:
​Quantify Supply Gaps: Without real-time tracking of "Average Demand" vs. "Average Availability," the company cannot accurately predict or mitigate "Supply Shortages."
​Link Operations to Finance: Financial teams see a "Total Loss" of 97K but cannot easily trace which supply chain inefficiencies or daily loss patterns (Average Daily Loss: 88.84) are driving those numbers.
​Manual Reporting Latency: Data residing in separate MySQL and SQL Server environments requires manual consolidation, leading to delayed decision-making.
​3. The Solution (Project Goal)
​The objective of this Power BI project is to develop an integrated Business Optimization Dashboard that:
​Extracts and Transforms: Pulls disparate data from MySQL and SQL Server into a single, cohesive data model.
​Visualizes Key Metrics: Provides at-a-glance KPIs for Profit/Loss and Supply Chain metrics to identify high-friction areas.
​Enables Data-Driven Decisions: Empowers stakeholders to reduce the "Total Supply Shortage" (currently at 579 units) by aligning availability more closely with daily demand.
### Steps followed 

- Step 1 :Installing MYSQL Server & MYSQL Workbench
- Step 2 : Understanding the Test Environment Data & Requirements
- Step 3  Importing the data in test environment in SQL Server
- Step 4 : Applying Left Join in SQL Server to prepare the data to be used for reporting

    create database test_env
  
    use test_env
  
     select * from [dbo].[Products]
  
    select * from [dbo].[Test Environment Inventory Dataset]
  
    select distinct demand from 
    [dbo].[Test Environment Inventory Dataset]
  
    select a.[Order_Date_DD_MM_YYYY],
    a.product_id,a.availability,a.demand,b.product_name,b.unit_price
    from [dbo].[Test Environment Inventory Dataset] as a
    left join products as b on a.product_id=b.product_id
  
   select * into new_table from 
   (select a.[Order_Date_DD_MM_YYYY],
   a.product_id,a.availability,a.demand,b.product_name,b.unit_price
  from [dbo].[Test Environment Inventory Dataset] as a
  left join products as b on a.product_id=b.product_id) x
  select * from new_table
 




- Step 5 : Importing the Data to Power BI Desktop from Test Environment
    

- Step 6 : Creating the DAX Measures & KPIs for Page 1
DAX Function:
- Step 7 : Create new measure as Average Demand Per Day
- 
DAX Function:

    Average Demand Per Day = DIVIDE([Total Demand],[Total Numbers of Days])

A Card chart was used to represent Average Demand Per Day:

- Step 8 : Create new measure as Average Availability Per Day

DAX Function;

    Average Availability Per Day = DIVIDE([Total Availabity],[Total Numbers of Days])

A Card chart was used to representA Average Availability Per Day:

- Step 9 : Create new measure as Total Supply Shortage

DAX Function:

    Total Supply Shortage = [Total Demand]-[Total Availabity]

A Card chart was used to representA Total Supply Shortage :

- Step 10 : Creating the DAX Measures & KPIs for Page 2

- Step 11 : Create new measure as Total Profit

DAX Function:

    Total Profit = SUMX(FILTER('Demand/Availability','Demand/Availability'[LOSS/PROFIT]>0),'Demand/Availability'[LOSS/PROFIT]*'Demand/Availability'[Unit_price])

A Card chart was used to representA  Total Profit :

- Step 12 : Create new measure as  TOTAL Loss

DAX Function :

    TOTAL Loss = SUMX(FILTER('Demand/Availability','Demand/Availability'[LOSS/PROFIT]<0),'Demand/Availability'[LOSS/PROFIT]*'Demand/Availability'[Unit_price])* -1

A Card chart was used to representA   TOTAL Loss :

- Step 13 : Create new measure as Average Loss Per Day

DAX Function ;

    Average Loss Per Day = DIVIDE([TOTAL Loss],[Total Numbers of Days])

A Card chart was used to representA  Average Loss Per Day :

- Step 14 : Importing Data into Production Environment in SQL Server

- Step 15 :  Data Cleaning using SQL & transitioning the report from test to Production

- Step 16 : Importing data into MYSQL Database

- Step 17 : Creating Equivalent SQL Code in MYSQL Workbench to populate New Table

- Step 18 : Creating Workspace & Publishing SQL Server Data Source's report

- Step 19 : Importing Data into Power BI Desktop from MYSQL Database

- Step 20 : Transitioning the report using Advanced Editor in Power Query Editor

- Step 20 : Data Validation & Publishing New report to MYSQL Database Workspace


# Insights

1) Average Demand Per Day = 3.40
2) Average Availability Per Day = 2.87
3) Total Supply Shortage = 579
4) Total Profit = 22k
5) Total Loss = 97K
6) Average Daily Loss = 88.84


   











