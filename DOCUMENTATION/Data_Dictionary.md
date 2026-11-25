# Data Dictionary - Indian Banking Credit and Loan Portfolio Analysis

## Source
Reserve Bank of India (RBI), Basic Statistical Return (BSR) data, republished on the India Data Portal (CKAN).
- India Data Portal dataset: https://ckandev.indiadataportal.com/dataset/reserve-bank-of-india
- RBI DBIE: https://data.rbi.org.in/ (BSR-1, BSR-2, Spatial Distribution of Deposits and Credit)
- RBI Handbook of Statistics on the Indian Economy, Tables 41-47, and Handbook of Statistics on Indian States, Tables 152-159, verified in the browser, direct XLSX links in Dataset_Sources.xlsx

All amounts are in Rs crore, as published by RBI. Outstanding credit and deposits are stocks as at end-March. Do not sum them across years.

This is aggregated data only. One credit row is a total for a whole Year x State x Bank Group x Sector cell, not one loan and not one borrower. There are no customer names, loan accounts, defaults, NPAs or repayment histories in this project, and none were added.

## Tables - 21,396 rows in total

### 1. Bank_Credit_Data.csv - 10,345 rows, 2015-2023
Grain: Year x State x Bank Group x Sector
- Record_ID - INT, Primary Key, unique, not null
- Year - INT, 2015 to 2023
- State - VARCHAR, 36 states
- State_Code - INT
- Bank_Group - VARCHAR, 6 groups: Public Sector, Private Sector, Foreign, Regional Rural, Small Finance, and one other group as per BSR
- Sector_or_Occupation - VARCHAR, 8 sectors: Personal Loans, Industry, Agriculture, Finance, Trade, Professional Services, Transport, All Others
- Number_of_Accounts - BIGINT
- Credit_Limit_Rs_Crore - DECIMAL
- Outstanding_Credit_Rs_Crore - DECIMAL

Aggregated by summing 1,233,985 genuine district-level BSR-1 rows, 2015-2023. No values invented.

### 2. Bank_Deposit_Data.csv - 7,096 rows, 2019-2022
Grain: Year x State x District x Population Group
- Record_ID - INT, Primary Key, unique, not null
- Year - INT, 2019 to 2022
- State - VARCHAR, 36 states
- State_Code - INT
- District - VARCHAR, 717 districts
- District_Code - INT
- Region - VARCHAR, 6 regions
- Population_Group - VARCHAR, 4 groups: Metropolitan, Urban, Semi-Urban, Rural
- Number_of_Accounts - BIGINT
- Deposit_Amount_Rs_Crore - DECIMAL

### 3. Bank_Branch_Data.csv - 3,205 rows, branches opened 2021-2023
Grain: One row per branch opened
- Branch_ID - VARCHAR, Primary Key, unique, not null
- Bank_Name - VARCHAR, 50 banks
- Bank_Group - VARCHAR, 5 groups
- State - VARCHAR, 33 states
- State_Code - INT
- District - VARCHAR
- District_Code - INT
- Branch_Type - VARCHAR, only BRANCH
- IFSC_Code - VARCHAR, blank in 302 rows, FSFB0000001 appears 358 times, so IFSC is not a unique key
- Year_Opened - INT, 2021: 735, 2022: 1,191, 2023: 1,279

### 4. Banking_Reference_Data.csv - 750 rows
Grain: One row per State + District
- State - VARCHAR
- State_Code - INT
- District - VARCHAR
- District_Code - INT
- Primary Key: State_Code + District_Code, composite. District_Code alone is not unique.

## Joins
- Credit to Deposit: Year + State_Code, state-year level only, overlapping years 2019-2022. Never join Credit to Deposit on Record_ID, the two Record_IDs are independent.
- Deposit to Reference: State_Code + District_Code, clean, 0 unmatched.
- Branch to Reference: State_Code + District_Code, clean, 0 unmatched.
- Credit to Branch: State_Code + Bank_Group, state level only.

## Data Quality Findings
- Row counts verified in SSMS: Credit 10,345, Deposit 7,096, Branch 3,205, Reference 750.
- Missing values in key columns: 0. Duplicate checks: 0.
- Credit: 202 rows with zero outstanding credit, 147 rows with zero credit limit, 72 rows where outstanding is greater than limit. No negative values.
- Deposit: 133 rows all-zero. No negative values.
- Branch: 302 rows with blank IFSC_Code.
- Deposit source had 7,060 all-zero duplicate rows in the raw file, cleaned as documented, totals unchanged.
- SSMS import note: SMALLINT overflows, deposit account count 40,420 is greater than 32,767. Use INT or BIGINT for counts, and DECIMAL for money.

## Limitations
- No borrower, interest rate, loan status, or default data, so this project cannot support loan-level default or credit-risk analysis.
- CD Ratio can only be calculated for 2019-2022, the years where both credit and deposits exist. Credit ends in 2023, deposits end in 2022.
- Year is a number, not a real date, so an Excel Timeline will not work. Use a Year Slicer instead.