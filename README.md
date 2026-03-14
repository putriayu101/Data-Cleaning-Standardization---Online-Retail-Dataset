# Data Cleaning Project - Online Retail Dataset

## 📌Project Overview
This project involves cleaning a **real-world online retail dataset** sourced from **Kaggle**. The raw data contained multiple quality issues including missing values, inconsistent formats, encoding errors, and multilingual entries across 6 columns.

**Goal:** Transform messy raw data into a clean, consistent, and analysis-ready dataset using Microsoft Excel.

## 📂Files
- online_retail_real_world.csv : RAW Dataset
- Dataset_Working-OnlineRetail.xlsm : Working file with all helper columns showing the cleaning process
- Dataset_Final-OnlienRetail.xlxs : Final claned dataset (output only)
- Note Cleaning Dataset.txt : Note cleaning process data

## 📊Dataset Information
- **Source:** Kaggle - Online Retail Real World Dataset
- **Total Rows:** 3.000 (after cleaning : 2.999)
- **Total Column:** 8
- **Columns:** OrderID, CustomerID, OrderDate, ProductName, Brand, Raw_Weight, 	Country, UnitPrice

## ⚠️Issues
|   **Column**   | **Issue**                              | **Count**  |
| -------------- | ---------------------------------------| ---------- |
|   UnitPrice    | Missing values                         |  386 rows  |
|   Raw_Weight   | Missing values + inconsisten format    |  513 rows  | 
|    Brand       | Missing values + encoding errors + inconsistent capitalization |   344 rows  |
|   ProductName  | Missing values + encoding errors + trademark symbols |  96 rows  |
|   OrderDate    | Missing value                          |  1 row     |
|   Country      | Missing value + multilingual names + irrelevant prefixes |  1 row  |

## 🔦Cleaning Process
1. **UnitPrice - Missing Values**
   - Calculate **Median** using **Array Formula** to exclude empty cells:
     **=MEDIAN(IF(H2:H3001>0,H2:H3001))**
   - Median result: **13.16**
   - Filled 386 empty cells using **CRTL+G -> Special -> Blanks**
     
2. **Raw_Weight - Inconsistent Format**
   - Created new column `Weight_Value` to extract numeric values using **LEFT, MIN, FIND formula**
   - Created new column `Weight_Unit` to extract unit labels
   - Created `Weight_Unit_Clean` to standardize units into: `g`, `kg`, `ml`, `l`, or `unknown`
   - **Result:** 2,394 rows standardized, 590 marked as `unknown` (513 originally empty, 77 undetermined)
     
3. **Brand - Encoding Rrrors & Inconsistency**
   - **Fixed broken Latin encoding** using **Find & Replace:**
      - `Ã©` → `é`
      - `â€™` → `'`
      - `Ã¨` → `è`
      - and more...
   - **Non-Latin characters (Arabic, Cyrillic, Emoji) were left as-is (out of cleaning scope)**
   - **Standardized capitalization** using `=PROPER(TRIM())`
   - Filled 334 empty cells with `Unknown`
4. **ProductName - Encoding & Missing Values**
   - **Removed broken trademark symbols (`Â®`, `â„¢`)** using **Find & Replace**
   - Filled **96 empty cells** with `Unknown`
   - **Standardized capitalization** using `=PROPER(TRIM())`

5. **OrderDate - Missing Value**
   - Deleted 1 empty row (0.03% of total data — not significant)

6. **Country - Multilingual & Format Issues**
   - **Removed irrelevant prefixes (`en:`, `fr:`, `de:`, `es:`)** using **Find & Replace**
   - **Standardized country names** to English:
      - `Maroc` → `Morocco`
      - `Argelia` → `Algeria`
      - `Frankreich` → `France`
      - and more...
   - **Standardized capitalization** using `=PROPER(TRIM())`
   - Filled 1 empty cell with `Unknown`


## ✅Result
|   **Column**   | **Before**                        |  **After**  |
| -------------- | ----------------------------------| ----------- |
|   UnitPrice    | 386 empty cells                   | All filled (median = 13.16) |
|   Raw_Weight   | 513 empty + inconsistent format   | Standardized to g/kg/ml/l) | 
|    Brand       | 344 empty + encoding errors       |  Clean + consistent capitalization  |
|   ProductName  | 96 empty + encoding errors        | Clean + consistent capitalization |
|   OrderDate    | 1 empty row                       |  Row deleted (3.000 -> 2.999) |
|   Country      | Multilingual + prefixes           |  Standardized to English  |

## 💡Notes
- Dataset contains multilingual entries (Arabic, Russian, French) — cleaning was focused on Latin character standardization and format consistency
- Raw_Weight entries with undetermined units were marked as unknown rather than assumed
- Two file versions were saved: working file (with helper columns) and final clean file

## 🧰Skills Demonstrated
- Handling missing values (median imputation, row deletion)
- Array Formula in Excel
- Find & Replace for encoding correction
- Text functions: PROPER(), TRIM(), LEFT(), MID(), FIND(), IFERROR()
- Data filtering and validation
- Column extraction and standardization

## 🌞About
This project is part of data portfolio.
📧putriayulw10@gmail.com 🌐https://www.linkedin.com/in/putriayulichawardani 

