# 🧹 Data Cleaning & Standardization - Online Retail Dataset
### Process
<img width="655" height="445" alt="RAW MESSY DATA" src="https://github.com/user-attachments/assets/e11cf625-5cec-41d8-a56b-2cd40446cf42" /> 
<img width="645" height="445" alt="Array formula2" src="https://github.com/user-attachments/assets/9a50c6c9-c18a-4551-933e-c17285e2dcef" />
<img width="645" height="445" alt="Before After" src="https://github.com/user-attachments/assets/19553755-ce7f-4b19-85b2-2b81d9faae8e" />
<img width="645" height="455" alt="Final dataset" src="https://github.com/user-attachments/assets/a4fc83c2-7810-4464-b68b-71e6d30bbd22" />


## 📌 Project Overview

This project demonstrates hands-on data cleaning skills applied to a real-world online retail dataset sourced from **Kaggle**. The raw data contained multiple quality issues including missing values, encoding errors, inconsistent formats, and multilingual entries across 6 columns.

**Goal:** Transform a messy, unstructured dataset into a clean, consistent, and analysis-ready file using Microsoft Excel — without any code or scripts.

## 📂 Files in This Repository

| File | Description |
|------|-------------|
| `Dataset_Working.xlsx` | Working file with all helper columns showing the step-by-step cleaning process |
| `Dataset_Final.xlsx` | Final cleaned dataset — output only, ready for analysis |
| `README.md` | Project documentation |

## 📊 Dataset Information

| Info | Detail |
|------|--------|
| Source | Kaggle — Online Retail Real World Dataset |
| Total Rows | 3,000 (after cleaning: 2,999) |
| Total Columns | 8 |
| Columns | OrderID, CustomerID, ProductName, Brand, Raw_Weight, Country, OrderDate, UnitPrice |


## ⚠️ Issues Found in Raw Data

| Column | Issue | Count |
|--------|-------|-------|
| UnitPrice | Missing values | 386 rows |
| Raw_Weight | Missing values + highly inconsistent format | 513 rows |
| Brand | Missing values + encoding errors + inconsistent capitalization | 334 rows |
| ProductName | Missing values + encoding errors + trademark symbols | 96 rows |
| OrderDate | Missing value | 1 row |
| Country | Missing value + multilingual names + irrelevant prefixes | 1 row + many rows |


## 🛠️ Cleaning Process

### 1. UnitPrice — Missing Values
- Calculated median using Array Formula to exclude empty cells:
  ```
  {=MEDIAN(IF($H$2:$H$3001>0,$H$2:$H$3001))}
  ```
- Median result: **13.16**
- Selected all blank cells using **Ctrl+G → Special → Blanks**, then filled with median value

### 2. Raw_Weight — Inconsistent Format
Raw values had many formats: `"100g"`, `"100 g"`, `"100 gram"`, `"1.7kg"`, `"350 g (x10)"`, `"48 oz"`, etc.

Steps taken:
- Created `Weight_Value` column to extract numeric part using:
  ```
  =IFERROR(VALUE(TRIM(LEFT(E2,MIN(FIND({" ","g","k","m","o"},E2&" gkmo"))-1))),0)
  ```
- Created `Weight_Unit` column to extract unit label
- Created `Weight_Unit_Clean` to standardize all units into: `g`, `kg`, `ml`, `l`, or `unknown`
- Used `SEARCH()` inside `IF()` to rescue additional rows with embedded unit characters

**Result:** 2,394 rows standardized, 590 marked as `unknown` (513 originally empty, 77 undetermined)

### 3. Brand — Encoding Errors & Inconsistency
- Fixed broken Latin encoding using Find & Replace:

| Find | Replace |
|------|---------|
| `Ã©` | `é` |
| `â€™` | `'` |
| `Ã¨` | `è` |
| `Ã‰` | `É` |
| `Â®` | *(removed)* |

- Non-Latin characters (Arabic, Cyrillic, Emoji) were intentionally left as-is (out of cleaning scope)
- Standardized capitalization using `=PROPER(TRIM())`
- Filled 334 empty cells with `Unknown`

### 4. ProductName — Encoding & Missing Values
- Removed broken trademark symbols (`Â®`, `â„¢`) via Find & Replace
- Filled 96 empty cells with `Unknown`
- Standardized capitalization using `=PROPER(TRIM())`

### 5. OrderDate — Missing Value
- Deleted 1 empty row — only 0.03% of total data, not worth imputing

### 6. Country — Multilingual & Format Issues
- Removed irrelevant prefixes (`en:`, `fr:`, `de:`, `es:`) via Find & Replace
- Standardized country names to English:

| Before | After |
|--------|-------|
| `Maroc` | `Morocco` |
| `Argelia` | `Algeria` |
| `Frankreich` | `France` |
| `Royaume-Uni` | `United Kingdom` |
| `Pays-Bas` | `Netherlands` |

- Standardized capitalization using `=PROPER(TRIM())`
- Filled 1 empty cell with `Unknown`


## ✅ Before & After Summary

| Column | Before | After |
|--------|--------|-------|
| UnitPrice | 386 empty cells | All filled (median = 13.16) |
| Raw_Weight | 513 empty + inconsistent formats | Standardized to g / kg / ml / l |
| Brand | 334 empty + encoding errors | Clean + consistent capitalization |
| ProductName | 96 empty + encoding errors | Clean + consistent capitalization |
| OrderDate | 1 empty row | Row deleted (3,000 → 2,999) |
| Country | Multilingual + prefixes | Standardized to English |


## 💡 Key Notes

- Dataset contains multilingual entries (Arabic, Russian, French) — cleaning was focused on Latin character standardization and format consistency. Non-Latin characters were left as-is and documented.
- Raw_Weight entries with undetermined units were marked as `unknown` rather than assumed — prioritizing data integrity over completeness.
- Two file versions delivered: working file (with helper columns for transparency) and final clean file (output only).


## 🧰 Excel Skills Demonstrated

- **Array Formula** — `MEDIAN(IF(...))` for conditional median calculation
- **Nested IF + SEARCH** — multi-condition text classification
- **LEFT + MIN + FIND** — extracting substrings from inconsistent text
- **PROPER + TRIM** — text standardization
- **IFERROR** — handling edge cases gracefully
- **Find & Replace** — bulk encoding correction
- **Ctrl+G Special → Blanks** — efficient bulk fill of missing values
- **Data Filter** — isolating and inspecting problem rows


## 🌻 About
This project is part of data analyst portfolio.

| | |
|--|--|
| 📧 Email | putriayulw10@gmail.com |
| 🌐 LinkedIn | https://www.linkedin.com/in/putriayulichawardani |


*This dataset was sourced from Kaggle for portfolio/practice purposes.*
