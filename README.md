# Indian Banking Credit and Loan Portfolio Analysis using SQL Server and Advanced Excel

> **Real-life data: Genuine data taken from the RBI website (data.rbi.org.in) - RBI BSR data, republished on the India Data Portal.**

Indian banking credit, deposits, and branch expansion, analysed from genuine RBI BSR data, 2015 to 2023, using SQL Server for analysis and Advanced Excel for the dashboard.

Image not found
Project Overview

This project analyses the credit and loan portfolio of Indian banks using genuine Reserve Bank of India (RBI) data. The work was done in two stages: SQL first, then Excel.

- SQL Server (SSMS): Data exploration, data cleaning, analysis, and business insights
- Advanced Excel: 11 PivotTables, a CD Ratio summary table, 5 PivotCharts, 8 KPI cards, and Year and State slicers
- Data: 21,396 rows in 4 tables, all amounts in Rs crore
- Period: Credit 2015-2023, Deposits 2019-2022, Branches opened 2021-2023
Data Source

Genuine RBI BSR data, via the India Data Portal (CKAN).

- India Data Portal dataset "Reserve Bank of India": https://ckandev.indiadataportal.com/dataset/reserve-bank-of-india
- RBI DBIE: https://data.rbi.org.in/ (BSR-1, BSR-2, Spatial Distribution of Deposits and Credit)
- RBI Handbook of Statistics on the Indian Economy, Tables 41-47, and Handbook of Statistics on Indian States, Tables 152-159

This is aggregated data only. One credit row is a total for a whole Year x State x Bank Group x Sector cell, not one loan and not one borrower. There are no customer names, loan accounts, defaults, NPAs, or repayment histories in this project, and none were added.

Datasets - 21,396 rows
Table	Rows	Period	Grain
Bank_Credit_Data.csv	10,345	2015-2023	Year x State x Bank Group x Sector
Bank_Deposit_Data.csv	7,096	2019-2022	Year x State x District x Population Group
Bank_Branch_Data.csv	3,205	2021-2023	One row per branch opened
Banking_Reference_Data.csv	750	-	One row per State + District
Key Findings

1. Total credit more than doubled: Outstanding credit rose from Rs 68,78,468 crore in 2015 to Rs 1,41,98,001 crore in 2023, a growth of 106.4%.

2. Deposits grew steadily: Total deposits rose from Rs 1,26,33,468 crore in 2019 to Rs 1,70,04,196 crore in 2022.

3. CD Ratio fell, then recovered slightly: 2019: 78.34%, 2020: 76.58%, 2021: 71.75%, 2022: 72.09%. CD Ratio can only be calculated for 2019-2022, the years where both credit and deposits exist.

4. Maharashtra leads credit: Top state by credit in 2023 is Maharashtra at Rs 33,32,738 crore, followed by Delhi at Rs 15,35,986 crore, Tamil Nadu at Rs 13,25,333 crore, Karnataka at Rs 10,27,656 crore, and Gujarat at Rs 8,28,364 crore.

5. Personal Loans is the largest sector: Top sector by credit in 2023 is Personal Loans at Rs 40,00,056 crore, followed by Industry at Rs 35,49,189 crore, and Agriculture at Rs 19,07,444 crore.

6. Mumbai leads deposits: Top district by deposits in 2022 is Mumbai at Rs 14,00,625 crore, followed by Bengaluru Urban at Rs 9,38,096 crore, and Mumbai Suburban at Rs 8,70,230 crore.

7. Andhra Pradesh has the highest CD Ratio: Top CD Ratio by state in 2022 is Andhra Pradesh at 142.71%, followed by Tamil Nadu at 103.69%, Telangana at 103.48%, and Delhi at 95.70%.

8. Uttar Pradesh opened the most branches: Branches opened 2021-2023 total 3,205 - 2021: 735, 2022: 1,191, 2023: 1,279. Top state is Uttar Pradesh with 329 branches, followed by Rajasthan with 287, Odisha with 261, Bihar with 260, and Maharashtra with 225.

Full findings are in DOCUMENTATION/Project_Insights.md. Full column, key, join, and data quality details are in DOCUMENTATION/Data_Dictionary.md.

Dashboard KPIs
- Total Credit 2023: Rs 1,41,98,001 crore
- Total Deposits 2022: Rs 1,70,04,196 crore
- CD Ratio 2022: 72.09%
- Branches Opened 2021-2023: 3,205
- Total Credit 2015: Rs 68,78,468 crore
- Credit Growth 2015-2023: 106.4%
- Top State Maharashtra: Rs 33,32,738 crore in 2023
- Top Sector Personal Loans: Rs 40,00,056 crore in 2023

Note: The Top State and Top Sector KPI cards on the Dashboard show the all-years totals, Rs 2,14,85,185 crore for Maharashtra and Rs 2,81,47,192 crore for Personal Loans, because the Year slicer is connected to those pivots. The 2023 values above are the correct single-year values.

Project Structure
Indian-Banking-Credit-Analysis/
├── DATASETS/
│   ├── Bank_Credit_Data.csv
│   ├── Bank_Deposit_Data.csv
│   ├── Bank_Branch_Data.csv
│   └── Banking_Reference_Data.csv
├── SQL/
│   ├── Data_Exploration.sql
│   ├── Data_Cleaning.sql
│   ├── Data_Analysis.sql
│   └── Bussiness_Insights.sql
├── EXCEL-DASHBOARD/
│   ├── Banking_Dashboard.xlsx
│   └── DASHBOARD.png
├── DOCUMENTATION/
│   ├── Data_Dictionary.md
│   └── Project_Insights.md
└── README.md
How to Run This Project
SQL - Microsoft SQL Server / SSMS
1. Create a database and import the 4 CSV files from DATASETS as CREDIT, DEPOSIT, BRANCH, and REFERENCE.
2. Use INT or BIGINT for counts and DECIMAL for money. SMALLINT overflows, deposit account count 40,420 is greater than 32,767.
3. Run the SQL files in order:
   - Data_Exploration.sql - row counts, missing values, duplicate checks
   - Data_Cleaning.sql - data quality checks, 202 zero outstanding credit, 147 zero limit, 302 blank IFSC
   - Data_Analysis.sql - 10 analysis tasks
   - Bussiness_Insights.sql - CD Ratio by year and by state, top districts by deposits, branches by state with credit
4. Join Credit to Deposit on Year + State_Code, state-year level only, overlapping years 2019-2022. Never join Credit to Deposit on Record_ID, the two Record_IDs are independent. Join Deposit and Branch to Reference on State_Code + District_Code.
Excel - Advanced Excel
1. Open EXCEL-DASHBOARD/Banking_Dashboard.xlsx.
2. Sheets: Banking_Dashboard, Credit_Data, Deposit_Data, Branch_Data, Reference_Data, Credit_Pivot, Deposit_Pivot, Branch_pivot, Summary_CD.
3. The workbook has 11 PivotTables, 5 PivotCharts, 8 KPI cards, and Year and State slicers on the Banking_Dashboard sheet.
4. Trend pivots use all years. Snapshot pivots use only the latest year for that dataset, 2023 for credit and 2022 for deposits, because using all years would sum 9 years together and be misleading.
Tools Used
- Microsoft SQL Server and SSMS
- Advanced Excel - PivotTables, PivotCharts, Slicers, KPI cards
- Data source: RBI BSR data via India Data Portal
Limitations
- No borrower, interest rate, loan status, or default data, so this project cannot support loan-level default or credit-risk analysis.
- CD Ratio can only be calculated for 2019-2022, the years where both credit and deposits exist. Credit ends in 2023, deposits end in 2022.
- Year is a number, not a real date, so an Excel Timeline will not work. Use a Year Slicer instead.
Author

Arsalan Shafi Wani - B.Sc. IT, MSc Data Science student, Chandigarh University. MIS Executive and Data Analyst, fresher.