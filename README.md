# Customer Churn Analysis — Power BI Dashboard

## 📌 Project Overview
A Power BI dashboard analyzing customer churn for a retail bank, built on a
10,000-customer dataset. The report identifies **who is leaving the bank,
where, and why** — surfacing patterns across demographics, geography, credit
behavior, and product usage to support retention strategy.

## 🎯 Purpose
Banks lose significant revenue when customers churn. This project explores
the churn dataset to answer:
- What percentage of customers are churning, and is it improving or worsening
  over time?
- Which customer segments (gender, age, geography, credit score, active
  status) churn the most?
- What early indicators (e.g. number of products held) correlate strongly
  with churn?

The goal is a self-service dashboard a bank manager could use to explore
churn drivers without needing to read raw data.

## 🛠️ Tech Stack
- Power BI Desktop — report building, data modeling, visualization
- Power Query (M) — data import and cleaning
- DAX — all measures (Total Customer, Churn%, Exit/Retain Customers,
  Active/Inactive splits, Credit Card Holder splits, time-intelligence
  Previous Month comparison, etc.)
- Star Schema Data Modeling — one fact table (Bank_Churn) connected to
  6 dimension tables (Geography, Gender, ActiveCustomer, Exit Customer,
  CreditCard, Date Master)
- Editor: Power BI Desktop (Windows)

## 📊 Data Source
- Dataset: Bank Customer Churn (Kaggle — "Churn Modelling" dataset)
- ~10,000 rows, 14 columns including CustomerId, CreditScore, Geography,
  Gender, Age, Tenure, Balance, NumOfProducts, HasCrCard, IsActiveMember,
  EstimatedSalary, Exited, and account join date

## 🗂️ Data Model / Table Workflow
Built as a star schema for clean, scalable reporting rather than a single
flat table:

1. Bank_Churn (fact table) — one row per customer, imported and cleaned
   via Power Query (removed row index, corrected data types, added a
   calculated Credit Score band column)
2. Dimension tables created to translate coded values into readable
   labels, each connected to Bank_Churn on a 1-to-many relationship:
   - Geography — GeographyID → Country name
   - Gender — GenderID → Male/Female
   - ActiveCustomer — IsActiveMember flag → Active/Inactive
   - Exit Customer — Exited flag → Exit/Retain
   - CreditCard — HasCrCard flag → Holder/Non-Holder
   - Date Master — a generated calendar table (Year, Month, Month order)
     built off the account join date, marked as an official date table to
     enable time-intelligence measures
3. Calculation (measures table) — a dedicated blank table holding every
   DAX measure (Total Customer, Active/Inactive, Credit Card Holder/
   Non-Holder, Exit/Retain Customers, Churn%, Previous Month Exit
   Customers), keeping all business logic in one place rather than
   scattered across tables
4. Relationships were built in Model view, connecting each dimension
   table's ID column to the matching column in Bank_Churn, forming the
   star schema all visuals report against

## ✨ Features & Highlights

### Problem
~20% of the bank's customers have churned. Leadership has no easy way to
see which segments are most at risk or how churn is trending month to
month.

### Goal
Build an interactive, two-page report that lets a non-technical user
filter by year, month, geography, gender, active status, and credit card
ownership, and immediately see churn KPIs and trends update.

### Walkthrough of Key Visuals

Page 1 — Overview
- 7 KPI cards: Total, Active/Inactive, Credit Card Holders/Non-Holders,
  Exit/Retain Customers
- Column chart: customer volume by year, split by active status
- Line chart: monthly exit trend vs. previous month, to spot
  improving/worsening periods
- Donut chart: churn split by gender
- Bar chart: churn by credit score band (Excellent → Poor)
- Pie chart: churn split by credit card ownership

Page 2 — Deep Dive
- Churn% matrix: year × month breakdown with conditional-formatting icons
  flagging high/low churn periods at a glance
- Column chart: exit vs. retain customers by geography (France, Germany,
  Spain)
- Line chart: exit vs. retain customers by age — shows churn risk peaks
  in a specific age band
- Area chart: exit customers and retain customers by month, added
  to compare how both trends move together across the year

### Key Insight
Churn is not evenly distributed — certain geographies, credit score
bands, and customer segments churn at meaningfully higher rates than
others, which the dashboard makes visible at a glance through filtering.

## 📂 Files
- Bank_Churn.csv — source dataset
- PROJECT_BANK_CHUNK_1.pbix — Power BI report file
- snapshots_of_dashboard1.png, snapshots_of_dashboard2.png — dashboard
  screenshots

## 🚀 How to Use
1. Open the .pbix file in Power BI Desktop
2. Use the slicers (Year, Month, Geography, Active Category, Exit
   Category, Gender) to filter the report
3. Navigate between pages using the tabs at the bottom

## Screenshots

1. <img width="1374" height="744" alt="snapshots_page_1" src="https://github.com/user-attachments/assets/48e47c54-f4a2-43db-ae82-d7857f53f708" />
2. <img width="1385" height="737" alt="snapshots page 2" src="https://github.com/user-attachments/assets/96036756-049e-42c4-923f-4363a5036852" />

