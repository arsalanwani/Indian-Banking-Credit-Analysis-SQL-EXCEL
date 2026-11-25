# Project Insights - Indian Banking Credit and Loan Portfolio Analysis

## Project Summary
Indian Banking Credit and Loan Portfolio Analysis using SQL Server and Advanced Excel, built from genuine RBI BSR data via the India Data Portal. 21,396 rows in 4 tables. SQL Steps 1-4 completed in SSMS, then 11 PivotTables, a Summary_CD table, 5 PivotCharts, 8 KPI cards, and Year and State slicers in Excel.

## Key Findings

### 1. Total credit more than doubled from 2015 to 2023
Total outstanding credit rose from Rs 68,78,468 crore in 2015 to Rs 1,41,98,001 crore in 2023, a growth of 106.4%. Credit grew every year, with the fastest growth in 2023.

### 2. Deposits grew steadily from 2019 to 2022
Total deposits rose from Rs 1,26,33,468 crore in 2019 to Rs 1,70,04,196 crore in 2022. Deposits grew every year in this period.

### 3. CD Ratio fell, then recovered slightly
Credit-Deposit Ratio by year: 2019: 78.34%, 2020: 76.58%, 2021: 71.75%, 2022: 72.09%. The ratio fell from 2019 to 2021, as deposits grew faster than credit, then rose slightly in 2022.

### 4. Maharashtra leads credit by a large margin
Top 5 states by credit in 2023: Maharashtra Rs 33,32,738 crore, Delhi Rs 15,35,986 crore, Tamil Nadu Rs 13,25,333 crore, Karnataka Rs 10,27,656 crore, Gujarat Rs 8,28,364 crore. Maharashtra alone is more than double Delhi.

### 5. Personal Loans is the largest sector
Top sector by credit in 2023 is Personal Loans at Rs 40,00,056 crore, followed by Industry at Rs 35,49,189 crore, and Agriculture at Rs 19,07,444 crore.

### 6. Mumbai leads deposits by district
Top 5 districts by deposits in 2022: Mumbai Rs 14,00,625 crore, Bengaluru Urban Rs 9,38,096 crore, Mumbai Suburban Rs 8,70,230 crore, New Delhi Rs 5,03,820 crore, Chennai Rs 4,85,836 crore.

### 7. Andhra Pradesh has the highest CD Ratio by state
Top CD Ratio by state in 2022: Andhra Pradesh 142.71%, Tamil Nadu 103.69%, Telangana 103.48%, Delhi 95.70%. A CD Ratio above 100% means credit in that state is higher than deposits in that state.

### 8. Uttar Pradesh opened the most branches
Branches opened 2021-2023: total 3,205, 2021: 735, 2022: 1,191, 2023: 1,279. Top state is Uttar Pradesh with 329 branches, followed by Rajasthan with 287, Odisha with 261, Bihar with 260, and Maharashtra with 225. Uttar Pradesh also had Rs 7,55,489 crore credit in 2023.

## KPI Cards - Dashboard
- Total Credit 2023: Rs 1,41,98,001 crore
- Total Deposits 2022: Rs 1,70,04,196 crore
- CD Ratio 2022: 72.09%
- Branches Opened 2021-2023: 3,205
- Total Credit 2015: Rs 68,78,468 crore
- Credit Growth 2015-2023: 106.4%
- Top State Maharashtra: Rs 33,32,738 crore in 2023, Rs 2,14,85,185 crore for all years 2015-2023
- Top Sector Personal Loans: Rs 40,00,056 crore in 2023, Rs 2,81,47,192 crore for all years 2015-2023

Note: The Top State and Top Sector KPI cards on the Dashboard show the all-years totals, because the Year slicer is connected to those pivots. The 2023 values above are the correct single-year values.

## Tools Used
- Microsoft SQL Server and SSMS: data exploration, cleaning, analysis, and business insights, 4 SQL files, 01 to 04
- Advanced Excel: 11 PivotTables, Summary_CD table, 5 PivotCharts, 8 KPI cards, Year and State slicers
- Data source: RBI BSR data via India Data Portal, https://ckandev.indiadataportal.com/dataset/reserve-bank-of-india
