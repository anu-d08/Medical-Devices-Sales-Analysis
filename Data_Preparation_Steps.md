# Data Preparation & Transformation Steps

### Source Files
The dataset was created from regional sales extracts covering North America, Europe, APAC, and LATAM.  
Each file contained fields for product name, sales amount, units sold, region, and date.  
The original data was confidential; an anonymized sample structure (`Medical_Devices_Sales_anonymized.csv`) is included for reference.

---

### Step 1: Data Consolidation
- Combined all regional sales CSVs into a single dataset using Power Query.  
- Ensured column names were standardized across all sources (`Product_Name`, `Region`, `Units_Sold`, `Revenue_USD`, `Date`).  
- Appended records and removed redundant headers left from merged files.

---

### Step 2: Data Cleaning
- Removed **duplicate rows** using Product + Region + Date as a composite key.  
- Filled missing `Units_Sold` values with zero where applicable.  
- Replaced null or inconsistent text fields with “Unknown” to maintain integrity.  
- Standardized region naming conventions: e.g., “N. America” → “North America.”  
- Converted all currency fields to USD for uniformity.

---

### Step 3: Feature Engineering (Calculated Columns)
Created new metrics in Power Query / DAX:
| **New Column** | **Formula / Logic** | **Purpose** |
|----------------|---------------------|--------------|
| `Total_Revenue` | `SUM(Revenue_USD)` | Aggregates regional revenue |
| `Total_Units_Sold` | `SUM(Units_Sold)` | Shows total product volume |
| `Avg_Of_Revenue` | `Total_Revenue / COUNT(Product_Name)` | Revenue per device |
| `Margin_Category` | IF `Avg_Of_Revenue` > median → “High Margin” else “Standard” | Categorizes profitability |

---

### Step 4: Data Validation
- Cross-checked total revenue and units against source extracts for accuracy.  
- Verified regional sums equal the global total.  
- Performed sanity checks:
  - No negative or zero revenue values.
  - Date field formats consistent (`YYYY-MM-DD`).
  - Product names and categories aligned across tables.

---

### Step 5: Data Modeling (Power BI) 
- Built measures using DAX for KPIs:
  - `Total Revenue`
  - `Total Units`
  - `Average Revenue`
  - `Revenue Share by Region`

---

### Step 6: Business Logic Verification
- Cross-checked calculated metrics with manual Excel pivot summaries.  
- Conducted random spot-checks for five sample products across all regions.  
- Ensured that KPI cards in Power BI match expected results from validation data.

---

### Step 7: Final Notes
  
- All transformations performed within Power Query; no external scripts used.  
- Dataset anonymized and sample version provided for portfolio demonstration.

---

**Author:Anu D 
**Tool:** Microsoft Power BI / Power Query / DAX  
**Date:** October 2025
