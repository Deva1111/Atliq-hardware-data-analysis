# AtliQ Hardware Sales Insights Dashboard

## Project Overview
This project involves performing data analysis on sales data from AtliQ Hardware, an India-based company that supplies computer hardware and peripherals to clients across the country. The goal is to create a Power BI dashboard that provides actionable insights into the company's sales performance.

## Problem Statement
AtliQ Hardware, headquartered in Delhi with regional offices throughout India, is experiencing declining overall sales. The Sales Director struggles to obtain a clear, data-driven view of the business performance due to fragmented and verbal reports from regional managers. The dynamic growth of the market necessitates a more robust and visual approach to track and analyze sales data.

## Solution
To address these challenges, a Power BI dashboard was created to provide a comprehensive view of the sales data. This dashboard enables the Sales Director to access real-time insights and make data-driven decisions to improve the company's sales performance.

## Data Source
The data used in this project is imported from an existing MySQL database. The following steps outline the process of data cleaning, ETL (Extract, Transform, Load), and data analysis performed in Power BI.

## Data Cleaning and ETL

### Step 1: Connect MySQL Database to Power BI
1. **Connect the MySQL database with Power BI Desktop.**
2. **Load the data into Power BI Desktop.** This step involves loading all tables from the database into the Power BI environment, forming the star schema model.

![image](https://github.com/Deva1111/Atliq-hardware-data-analysis/assets/125787421/1c4feadb-4b32-45dd-ae41-db2e114573da)


### Step 2: Data Transformation using Power Query
1. **Filter Data in Markets Table:**
   - Remove rows with null values and deselect blank options.
   
2. **Filter Data in Transactions Table:**
   - Exclude negative and zero values to clean the data.

3. **Convert USD to INR in Transactions Table:**
   - AtliQ Hardware operates only in India; hence, transactions in USD were converted to INR.
   - Formula used: '=Table.AddColumn(#"Filtered Rows", "norm_sales_amount", each if [currency] = "USD" then [sales_amount]*80 else [sales_amount])

4. **Remove Duplicate Currency Records:**
   - Identified and removed duplicate currency records in the transactions table to ensure data integrity.

## Data Modeling
After cleaning and transforming the data, it was ready for modeling. The data tables were structured to support effective analysis and visualization in Power BI.

## Data Analysis (DAX)
Key measures used in the dashboard visualizations include:

- **Profit Margin %:** `DIVIDE([Total Profit Margin], [Revenue], 0)`
- **Profit Margin Contribution %:** `DIVIDE([Total Profit Margin], CALCULATE([Total Profit Margin], ALL('sales products'), ALL('sales customers'), ALL('sales markets')))`
- **Revenue:** `SUM('sales transactions'[sales_amount])`
- **Revenue Contribution %:** `DIVIDE([Revenue], CALCULATE([Revenue], ALL('sales products'), ALL('sales customers'), ALL('sales markets')))`
- **Revenue LY:** `CALCULATE([Revenue], SAMEPERIODLASTYEAR('sales date'[date]))`
- **Sales Quantity:** `SUM('sales transactions'[sales_qty])`
- **Total Profit Margin:** `SUM('Sales transactions'[Profit_Margin])`
- **Profit Target:**
  - **Profit Target1:** `GENERATESERIES(-0.05, 0.15, 0.01)`
  - **Profit Target Value:** `SELECTEDVALUE('Profit Target1'[Profit Target])`
  - **Target Diff:** `[Profit Margin %] - 'Profit Target1'[Profit Target Value]`

## Dashboard Overview

![Screenshot 2024-06-28 222345](https://github.com/Deva1111/Atliq-hardware-data-analysis/assets/125787421/c233068c-6ab7-41a0-b278-8d64a83922cc)


The dashboard provides insights into:
- Total Revenue and Sales Quantity
- Revenue and Sales Quantity by Markets
- Revenue Trend Over Time
- Top 5 Customers and Products

## Conclusion
By utilizing Power BI for data visualization, AtliQ Hardware can now access real-time sales insights, enabling data-driven decision-making and potentially reversing the decline in sales. This project demonstrates the power of data analytics in driving business performance.

## Usage
To use this dashboard, follow these steps:
1. Load the provided '.pbix' file into Power BI Desktop.
2. Ensure you have access to the MySQL database and update the connection settings if necessary.
3. Explore the various visuals and insights provided in the dashboard.


*Created by [Devendra Pardhi]*


