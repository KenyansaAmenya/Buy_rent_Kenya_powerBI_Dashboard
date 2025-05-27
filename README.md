# Kenya Real Estate Data Model - Power BI Project
## Project Overview
This Power BI project analyzes Kenyan real estate data, including property listings, owner details, tax information, and utility costs. The data model follows a star schema design with `Houses` as the central fact table.

# Data Sources
1. `houses_for_sale_kenya.csv` - Property listings
2. `owners_details.csv` - Owner information
3. `property_tax.csv` - Tax records
4. `house_utilities.csv` - Utility costs

# Data Cleaning Process
Before loading into Power BI, the raw data was preprocessed:
- Removed all "N/A" values and replaced with `0`
- Removed text labels ("bedrooms", "bathrooms", "KShs") from numeric fields
- Converted all relevant columns to integers
- Standardized PropertyID across all datasets

# Power BI Implementation Guide

# 1. Data Loading
1. Open Power BI Desktop
2. Go to: `Home → Get Data → Text/CSV`
3. Load all four CSV files
4. Rename tables appropriately:
   - `houses_for_sale_kenya` → `Houses`
   - `owners_details` → `Owners`
   - `property_tax` → `Taxes`
   - `house_utilities` → `Utilities`

# 2. Data Model Relationships
Establish these relationships in Model View:

| From Table  | Column     | To Table | Column     | Relationship | Cardinality  |
|-------------|------------|----------|------------|--------------|--------------|
| Owners      | PropertyID | Houses   | PropertyID | Many-to-One  | Single → 🔄  |
| Taxes       | PropertyID | Houses   | PropertyID | Many-to-One  | Single → 🔄  |
| Utilities   | PropertyID | Houses   | PropertyID | Many-to-One  | Single → 🔄  |

# 3. Key Measures
Created in the data model:
// Average House Price
Average Price = AVERAGE(Houses[Price])

// Total Annual Tax
Total Tax = SUM(Taxes[AnnualTaxAmount])

// Monthly Utility Cost
Total Utilities = SUM(Utilities[MonthlyElectricityCost]) + 
                  SUM(Utilities[MonthlyWaterCost]) +
                  SUM(Utilities[MonthlyInternetCost])
# 4. Visualizations
The report includes:

- Pie chart: Houses distribution by County

- Bar chart: Average tax per County

- Table: Owner information with property locations

 - KPI cards: Total properties and average utility costs
```dax
// Average House Price
Average Price = AVERAGE(Houses[Price])

// Total Annual Tax
Total Tax = SUM(Taxes[AnnualTaxAmount])

// Monthly Utility Cost
Total Utilities = SUM(Utilities[MonthlyElectricityCost]) + 
                  SUM(Utilities[MonthlyWaterCost]) +
                  SUM(Utilities[MonthlyInternetCost])
# 4. Visualizations
The report includes:

- Pie chart: Houses distribution by County

- Bar chart: Average tax per County

- Table: Owner information with property locations

 - KPI cards: Total properties and average utility costs

# 5. Data model diagram

                   +--------------+
                   |   Owners     |
                   |--------------|
                   | OwnerID      |
                   | PropertyID FK|
                   +--------------+
                         |
                         |
                         ▼
                   +--------------+
                   |   Houses     |◄────────+
                   |--------------|         |
                   | PropertyID PK|         |
                   +--------------+         |
                         ▲                  |
                         |                  |
                +--------+--------+  +------+------+
                |     Taxes       |  |  Utilities  |
                |-----------------|  |-------------|
                | PropertyID  FK  |  | PropertyID FK|
                +-----------------+  +--------------+
# 6. How to interact with my dashboard
# Usage Instructions
- Open the .pbix file in Power BI Desktop

- Refresh data connection if needed

- Interact with filters and slicers

- Hover over visuals for tooltips
# Challenges & Solutions
1. Data Quality Issues i.e Inconsistent formatting in raw data (e.g., "3 bedrooms" as text, "KSh 5,000,000" as strings).
Solution:
- Used Power Query to remove text labels (bedrooms, bathrooms, KShs) via Replace Values.
- Converted numeric fields (Price, Size) to integers by stripping commas and symbols.
- Replaced "N/A" values with 0 to avoid null errors in calculations.

2. Relationship Errors
The problem was that Power BI auto-detected incorrect relationships (e.g., many-to-many between Houses and Utilities).
- I solved this problem by manually setting all relationships to Many-to-One (Utilities → Houses).
- Verified PropertyID had unique values in the Houses table (no duplicates).
# What i learnt in this project is that:
- Always validate data types and relationships before building visuals.
- Use View > Performance Analyzer in Power BI to identify bottlenecks.
- Document all transformations in Power Query for reproducibility.

# Final Dashboard screenshot

![2025-05-28 00 35 46](https://github.com/user-attachments/assets/7b765e13-d65d-4005-b5e0-53b67b6022cb)
