# 🧹 Excel Data Cleaning Project — Audible Dataset

## 🧩 PROJECT GOAL  
**Turn raw, messy data → into clean, analysis-ready data, using only Excel formulas.**

This project demonstrates how to transform unstructured audiobook data into a structured, analysis-ready format — without using Power Query or VBA, focusing purely on **Excel formulas** like `TRIM`, `TEXTSPLIT`, `SUBSTITUTE`, `VALUE`, `SEARCH`, `LEFT`, `MID`, `IFERROR`, and more.

---
! [Audible_uncleaned](Audible_Data_Wrangling/Images/Audible_Uncleaned.png) 
! [Audible_cleaned](Audible_Data_Wrangling/Images/Audible_Cleaned.png)  
## 📊 Dataset Overview  

| Column | Example | Description |
|:--|:--|:--|
| **name** | Geronimo Stilton #11 & #12 | Audiobook title |
| **author** | Writtenby:GeronimoStilton | Author name, includes extra text |
| **narrator** | Narratedby:BillLobely | Narrator name, includes prefix |
| **time** | 13 hrs and 8 mins | Duration as text |
| **releasedate** | 04-08-08 | Date, inconsistent format (DD-MM-YY?) |
| **language** | English | Language |
| **stars** | 4.5 out of 5 stars41 ratings | Combined rating and review count |
| **price** | 1,256.00 | Numeric field stored as text, includes commas |

---

## 🚨 Step 1: Identify Unclean Data (Problems Found)

| Column | Issue Description | Example |
|:--|:--|:--|
| **name** | Some names may have trailing spaces, special characters, or mixed case | “ The Hunger Games: Special Edition ” |
| **author** | Has prefix “Writtenby:” and no spaces between first/last names | “Writtenby:RickRiordan” |
| **narrator** | Has prefix “Narratedby:” and no spaces | “Narratedby:RobbieDaymond” |
| **time** | Stored as text with inconsistent patterns (“10 hrs”, “11 hrs and 16 mins”) — cannot calculate directly | “13 hrs and 8 mins” |
| **releasedate** | Stored as text (DD-MM-YY), may misinterpret based on region | “04-08-08” |
| **language** | Inconsistent casing (“english”, “ENGLISH”, “English”) | “english” |
| **stars** | Mixed data — rating + review count combined | “4.5 out of 5 stars41 ratings” |
| **price** | Contains commas, stored as text, not numeric | “1,256.00” |

---

## 🧠 Step 2: Cleaning Approach (Using Formulas Only)

Each issue was addressed using Excel formulas — no Power Query, no VBA.

| Problem | Formula Used | Description |
|:--|:--|:--|
| Remove extra spaces | `=TRIM(A2)` | Removes extra spaces from text |
| Remove prefix (Writtenby / Narratedby) | `=SUBSTITUTE(A2,"Writtenby:","")` | Removes unwanted prefixes |
| Combine & manage columns | `=VSTACK(A1#,B1#)` | Combines or stacks split data into one column |
| Separate columns for cleaning | `=CHOOSECOLS(Audible_Cleaned!C5#,7)` | Extracts a specific column to a new sheet for cleaning |
| Split First & Last Names (joined by capital letters) | Formula using `TEXTSPLIT` or pattern detection with `MID` + `SEARCH` | Detects capital letters and splits names |
| Extract numeric hours | `=LEFT(A2,FIND("hrs",A2)-1)` | Extracts numeric duration |
| Convert text date | `=TEXT(A2,"yyyy-mm-dd")` | Converts inconsistent text date formats |
| Clean case (capitalize) | `=PROPER(A2)` | Converts all text into proper case |
| Extract rating | `=LEFT(A2,FIND("out of",A2)-2)` | Extracts “4.5” from “4.5 out of 5 stars” |
| Extract review count | `=MID(A2,FIND("stars",A2)+5,FIND("ratings",A2)-FIND("stars",A2)-5)` | Extracts “41” from “stars41 ratings” |
| Convert price to numeric | `=VALUE(SUBSTITUTE(A2,",",""))` | Removes commas and converts to number |
| Handle missing or invalid values | `=IFERROR(formula,"")` | Avoids #VALUE! errors when data is missing |

---

## 🧩 Step 3: Expected “Cleaned” Columns

| Column | Cleaned Example |
|:--|:--|
| **name** | The Hunger Games: Special Edition |
| **author** | Suzanne Collins |
| **narrator** | Tatiana Maslany |
| **duration_hours** | 10.58 |
| **releasedate** | 2018-10-30 |
| **language** | English |
| **rating** | 4.5 |
| **reviews** | 41 |
| **price** | 1256.00 |

---

## 🧱 Step 4: Project Deliverables

| File / Sheet | Description |
|:--|:--|
| **Audible_Uncleaned** | The original uncleaned dataset |
| **Audible_cleaned_final** | The fully cleaned, structured dataset |
| **Findings** | Dashboard-style summary containing: <br>• Total Audio Books <br>• Total Unique Books <br>• English books <br>• Other Language Books <br>• Average Price <br>• Number Of Books Rated  <br>• Non Rated Books |

---

## 🧾 Insights After Cleaning (Example)

| Metric | Value |
|:--|:--|
| **Total Audio Books** | 87489 |
| **Total Unique Books** | 82670 |
| **English books** | 61884 |
| **Other Language Books** | 25605|
| **Average Price (₹)** | ₹ 560.94 |
| **Number Of Books Rated ** | 15072 |
| **Non Rated Books** | 72417 |

---

## 🧮 Excel Functions Used

| Function | Purpose |
|:--|:--|
| **TRIM** | Removes unwanted extra spaces |
| **SUBSTITUTE** | Replaces unwanted text (e.g., removes “Writtenby”) |
| **PROPER** | Converts text into title case (first letter capitalized) |
| **TEXTSPLIT** | Splits text based on space or pattern |
| **LEFT / MID / FIND** | Extracts specific portions of text |
| **VALUE** | Converts text numbers into real numeric values |
| **IFERROR** | Prevents formula errors with cleaner output |
| **VSTACK** | Combines multiple column results into one |
| **CHOOSECOLS** | Extracts specific columns for cleaning or analysis |
| **TEXT** | Converts and formats date or numeric values |

---

## 💡 Key Learnings
- How to **detect**, **clean**, and **transform unstructured data** in Excel using formulas only  
- Hands-on understanding of **text manipulation**, **error handling**, and **data preparation logic**  
- Building a **formula-based cleaning workflow** ready for Power BI or further SQL analysis  

---

## 🧰 Tools Used
- **Microsoft Excel (Formulas Only)**
- **Excel Functions:** `TRIM`, `SUBSTITUTE`, `LEFT`, `RIGHT`, `MID`, `FIND`, `PROPER`, `VALUE`, `TEXT`, `VSTACK`, `CHOOSECOLS`, `IFERROR`

---

## 🏁 Final Outcome
> A **fully cleaned and analysis-ready Audible dataset** built **100% with Excel formulas**, demonstrating advanced data transformation, error handling, and text manipulation techniques.

---

## 🧑‍💻 Author
**[Marikannan]**  
Data Analyst | Excel | Power BI | SQL | Python  
