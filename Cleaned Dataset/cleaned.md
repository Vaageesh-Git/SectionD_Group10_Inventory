# Data Cleaning Report  
## Store-Specific Demand Forecasting – Rossmann Dataset  

---

## 1. Overview

The raw dataset contained inconsistencies in date formats, missing values, mixed data types, currency symbols, and categorical irregularities.  

To ensure accurate analysis and forecasting, structured data cleaning and preprocessing steps were performed on each column.

---

# Column-Wise Data Cleaning Summary

---

## 1️⃣ Store

**Issues Identified:**
- No major inconsistencies.
- Verified as numerical identifier.

**Cleaning Performed:**
- Converted to integer type.
- Checked for duplicate Store–Date combinations.
- Verified no missing Store IDs.

**Final Data Type:** Integer  
**Purpose:** Unique store identifier for store-level forecasting.

---

## 2️⃣ DayOfWeek

**Issues Identified:**
- Mixed formats such as:
  - `6`
  - `6 day`
  - `7 day`

**Cleaning Performed:**
- Removed text values like "day".
- Extracted numeric value only.
- Standardized values between 1–7.
- Converted to integer.

**Final Data Type:** Integer  
**Purpose:** Weekly seasonality analysis.

---

## 3️⃣ Date

**Issues Identified:**
- Multiple inconsistent formats:
  - `24/05/15`
  - `2013-03-26`
  - `13.07.23`
- Mixed separators (`/`, `-`, `.`)

**Cleaning Performed:**
- Standardized all dates into ISO format: `YYYY-MM-DD`
- Converted column to datetime type.
- Extracted additional time features:
  - Year
  - Month
  - Week
  - Day

**Final Data Type:** DateTime  
**Purpose:** Time-series forecasting and seasonal analysis.

---

## 4️⃣ Sales

**Issues Identified:**
- Currency symbol `$`
- Comma separators (e.g., `$5,548.00`)
- Missing values
- Zero sales on closed days

**Cleaning Performed:**
- Removed `$` symbol.
- Removed comma separators.
- Converted to numeric (float).
- Replaced missing values with:
  - 0 if store was closed
  - Investigated otherwise
- Verified logical condition:
  - If Open = 0 → Sales = 0

**Final Data Type:** Float  
**Purpose:** Target variable for forecasting.

---

## 5️⃣ Customers

**Issues Identified:**
- Missing values.
- Blank entries.
- Zero customers when store closed.

**Cleaning Performed:**
- Converted to numeric.
- Filled missing values using:
  - Median customer count per store (if store open)
  - 0 if store closed
- Verified correlation between Customers and Sales.

**Final Data Type:** Integer  
**Purpose:** Demand behavior and conversion rate analysis.

---

## 6️⃣ Open

**Issues Identified:**
- Binary values (0, 1).

**Cleaning Performed:**
- Ensured binary format:
  - 0 = Closed
  - 1 = Open
- Verified consistency with Sales column.

**Final Data Type:** Integer (Binary)  
**Purpose:** Store operational filtering.

---

## 7️⃣ Promo

**Issues Identified:**
- Mixed values:
  - `0`
  - `1`
  - `Active`

**Cleaning Performed:**
- Converted "Active" to 1.
- Standardized values:
  - 0 = No Promotion
  - 1 = Promotion Active
- Converted to integer.

**Final Data Type:** Integer (Binary)  
**Purpose:** Analyze promotional impact on sales.

---

## 8️⃣ StateHoliday

**Issues Identified:**
- Mixed encoding (numeric and categorical).

**Cleaning Performed:**
- Standardized values:
  - 0 = No Holiday
  - Other values treated as Holiday categories
- Converted to categorical type.
- Created binary holiday flag if required.

**Final Data Type:** Categorical  
**Purpose:** Holiday impact analysis.

---

## 9️⃣ SchoolHoliday

**Issues Identified:**
- Binary values (0,1).

**Cleaning Performed:**
- Converted to integer.
- Verified distribution and consistency.

**Final Data Type:** Integer (Binary)  
**Purpose:** Seasonal demand analysis.

---

# Additional Data Quality Checks

- Removed duplicate records.
- Checked and handled null values across columns.
- Verified logical relationships:
  - If Open = 0 → Sales = 0
  - If Sales > 0 → Customers > 0
- Identified and handled outliers in Sales using IQR method.
- Sorted dataset by Store and Date for time-series modeling.

---

# Final Dataset Status

- All date formats standardized.
- Monetary values converted to numeric.
- Categorical variables encoded properly.
- Missing values handled.
- Dataset ready for:
  - Exploratory Data Analysis (EDA)
  - Time-Series Forecasting
  - Inventory Optimization Modeling

---

# Conclusion

The dataset has been cleaned and standardized to ensure reliability and consistency for downstream analysis. Proper preprocessing ensures accurate forecasting results and meaningful business insights.