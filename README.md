# 🧹 Data Cleaning & Standardization - Online Retail Dataset

> Transformed a messy, real-world 3,000-row retail dataset into a clean, consistent, analysis-ready file using **Microsoft Excel only**, with no code or scripts.

## 🎯 Key Results

- **1,331 missing values resolved across 6 columns** (386 unit prices, 513 weights, 334 brands, 96 product names, 1 country, 1 order date), whether imputed, labeled `Unknown`, or removed
- **386 missing unit prices** imputed using the median value (13.16), calculated with a conditional array formula
- **2,394 inconsistent weight entries** (e.g., `"100 gram"`, `"1.7kg"`, `"350 g (x10)"`) standardized into a numeric value and a clean unit (`g`, `kg`, `ml`, `l`)
- **590 weight entries with no determinable unit** labeled `unknown` instead of guessed, prioritizing data integrity over completeness
- **430 missing brand and product names** labeled `Unknown` (334 + 96), after repairing encoding errors and unifying capitalization
- **Multilingual country names** (French, Spanish, German, etc.) translated to English and cleaned of language prefixes
- **3,000 → 2,999 rows:** 1 record with a missing order date removed (0.03% of the data)
- Delivered **two versions**: a working file with helper columns (every step traceable) and a final output-only file

## 📌 Project Overview

This project demonstrates hands-on data cleaning skills applied to a real-world online retail dataset sourced from **Kaggle**. The raw data contained multiple quality issues, including missing values, encoding errors, inconsistent formats, and multilingual entries across 6 of its 8 columns.

**Goal:** Transform a messy, unstructured dataset into a clean, consistent, and analysis-ready file using Microsoft Excel, without any code or scripts.

## 📂 Files in This Repository

| File | Description |
| ---- | ----------- |
| `online_retail_real_world.csv` | Original raw dataset (as downloaded from Kaggle) |
| `Dataset_Working-OnlineRetail.xlsm` | Working file with all helper columns showing the step-by-step cleaning process |
| `Dataset_Final-OnlineRetail.xlsx` | Final cleaned dataset, output only, ready for analysis |
| `Note Cleaning Dataset.md` | Step-by-step workflow of how the project was carried out |
| `Sales Report Presentation.pdf` | [ADD: one sentence describing what this PDF contains] |
| `README.md` | Project documentation |

## 📊 Dataset Information

| Info | Detail |
| ---- | ------ |
| Total Rows | 3,000 (after cleaning: 2,999) |
| Total Columns | 8 |
| Columns | OrderID, CustomerID, ProductName, Brand, Raw_Weight, Country, OrderDate, UnitPrice |

## ⚠️ Issues Found in Raw Data

| Column | Issue | Count |
| ------ | ----- | ----- |
| UnitPrice | Missing values | 386 rows |
| Raw_Weight | Missing values + highly inconsistent format | 513 rows |
| Brand | Missing values + encoding errors + inconsistent capitalization | 334 rows |
| ProductName | Missing values + encoding errors + trademark symbols | 96 rows |
| OrderDate | Missing value | 1 row |
| Country | Missing value + multilingual names + irrelevant prefixes | 1 row + many rows |

## 🛠️ Cleaning Process

### 1. UnitPrice: Missing Values

- Calculated the median using an Array Formula to exclude empty cells:

  ```
  {=MEDIAN(IF($H$2:$H$3001>0,$H$2:$H$3001))}
  ```

- Median result: **13.16**
- Selected all blank cells using **Ctrl+G → Special → Blanks**, then filled them with the median value

### 2. Raw_Weight: Inconsistent Format

Raw values came in many formats: `"100g"`, `"100 g"`, `"100 gram"`, `"1.7kg"`, `"350 g (x10)"`, `"14.4 oz (408g)"`, etc.

Steps taken:

- Created a `Weight_Value` column to extract the numeric part using:

  ```
  =IFERROR(VALUE(TRIM(LEFT(E2,MIN(FIND({" ","g","k","m","o"},E2&" gkmo"))-1))),0)
  ```

- Created a `Weight_Unit` column to extract the unit label
- Created a `Weight_Unit_Clean` column to standardize all units into: `g`, `kg`, `ml`, `l`, or `unknown`
- Used `SEARCH()` inside `IF()` to rescue additional rows with embedded unit characters
- For entries that list both imperial and metric values (e.g., `14.4 oz (408g)`), used the metric value in parentheses (`408 g`)

**Result:** 2,394 rows standardized, 590 marked as `unknown` (513 originally empty, 77 undetermined), and 15 rows left unchanged.

> **Note on the 15 unchanged rows:** these entries contain garbled text with no identifiable unit or weight (e.g., `Ð¨Ð¾Ðºð¾Ð»Ð°Ð´ 85% Ðºð°Ðºð°Ð¾Ð²Ð° Ð¼Ð°ÑÐ°`, a corrupted Cyrillic string), so they could not be standardized without guessing. They are documented here rather than forced into a category.

### 3. Brand: Encoding Errors & Inconsistency

- Fixed broken Latin encoding using Find & Replace:

| Find | Replace |
| ---- | ------- |
| `Ã©` | `é` |
| `â€™` | `'` |
| `Ã¨` | `è` |
| `Ã‰` | `É` |
| `Â®` | *(removed)* |

- Non-Latin characters (Arabic, Cyrillic, Emoji) were intentionally left as-is (out of cleaning scope)
- Standardized capitalization using `=PROPER(TRIM())`
- Filled 334 empty cells with `Unknown`

### 4. ProductName: Encoding & Missing Values

- Removed broken trademark symbols (`Â®`, `â„¢`) via Find & Replace
- Filled 96 empty cells with `Unknown`
- Standardized capitalization using `=PROPER(TRIM())`

### 5. OrderDate: Missing Value

- Deleted 1 empty row. It was only 0.03% of the total data, so it was not worth imputing.

### 6. Country: Multilingual & Format Issues

- Removed irrelevant prefixes (`en:`, `fr:`, `de:`, `es:`) via Find & Replace
- Standardized country names to English:

| Before | After |
| ------ | ----- |
| `Maroc` | `Morocco` |
| `Argelia` | `Algeria` |
| `Frankreich` | `France` |
| `Royaume-Uni` | `United Kingdom` |
| `Pays-Bas` | `Netherlands` |

- Standardized capitalization using `=PROPER(TRIM())`
- Filled 1 empty cell with `Unknown`

## 🧠 Decisions & Rationale

| Decision | Why |
| -------- | --- |
| Filled missing UnitPrice with the **median** (13.16) | Estimating a price for each individual product would require guessing, and a wrong guess on price is costly. The median is a neutral central value that is not distorted by extreme prices. |
| Labeled undeterminable weights as `unknown` | Assuming a unit could silently corrupt the data. An honest `unknown` is safer than a confident wrong value. |
| Used the metric value in entries like `14.4 oz (408g)` | The metric value is already given in the raw data, so no conversion or assumption was needed, and it keeps units consistent (`g`). |
| Deleted the row with a missing OrderDate | A single row (0.03%) has negligible impact, and a date cannot be reliably imputed. |
| Left non-Latin characters as-is | Cleaning focused on Latin-character standardization and format consistency; non-Latin text is valid data, not noise. |
| Left 15 unreadable weight entries unchanged | No unit could be identified, and forcing a value would mean guessing. |

## ⚠️ Limitations

- The 386 imputed unit prices are **placeholders, not true prices**. Any revenue or price analysis built on this dataset should treat them as estimates.
- The 590 `unknown` weights and 15 unchanged entries mean weight-based analysis covers 2,394 of 2,999 rows.
- Non-Latin entries (Arabic, Cyrillic, Emoji) were not translated or transliterated.

## ✅ Before & After Summary

| Column | Before | After |
| ------ | ------ | ----- |
| UnitPrice | 386 empty cells | All filled (median = 13.16) |
| Raw_Weight | 513 empty + inconsistent formats | Standardized to g / kg / ml / l (2,394), `unknown` (590), unchanged (15) |
| Brand | 334 empty + encoding errors | Clean + consistent capitalization |
| ProductName | 96 empty + encoding errors | Clean + consistent capitalization |
| OrderDate | 1 empty row | Row deleted (3,000 → 2,999) |
| Country | Multilingual + prefixes | Standardized to English |

## 📸 Process Screenshots

<!-- Keep your existing image links below; add the captions underneath each one. -->

**1. Raw messy data**
<img width="755" height="445" alt="RAW MESSY DATA" src="https://github.com/user-attachments/assets/e11cf625-5cec-41d8-a56b-2cd40446cf42" /> <br>

**2. Array formula for the median**
<img width="755" height="445" alt="Array formula2" src="https://github.com/user-attachments/assets/9a50c6c9-c18a-4551-933e-c17285e2dcef" /><br>

**3. Before and after**
<img width="755" height="445" alt="Before After" src="https://github.com/user-attachments/assets/19553755-ce7f-4b19-85b2-2b81d9faae8e" />
<br>

**4. Final dataset**
<img width="755" height="455" alt="Final dataset" src="https://github.com/user-attachments/assets/a4fc83c2-7810-4464-b68b-71e6d30bbd22" />
<br>

## 🧰 Excel Skills Demonstrated

- **Array Formula**: `MEDIAN(IF(...))` for conditional median calculation
- **Nested IF + SEARCH**: multi-condition text classification
- **LEFT + MIN + FIND**: extracting substrings from inconsistent text
- **PROPER + TRIM**: text standardization
- **IFERROR**: handling edge cases gracefully
- **Find & Replace**: bulk encoding correction
- **Ctrl+G Special → Blanks**: efficient bulk fill of missing values
- **Data Filter**: isolating and inspecting problem rows

## 🌻 About

This project is part of my data analyst portfolio.

|  |  |
| -- | -- |
| 📧 Email | [putriayulw10@gmail.com](mailto:putriayulw10@gmail.com) |
| 🌐 LinkedIn | [linkedin.com/in/putriayulichawardani](https://www.linkedin.com/in/putriayulichawardani) |

*This dataset was sourced from Kaggle for portfolio/practice purposes.*
