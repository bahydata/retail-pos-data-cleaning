## Project: Data Cleaning - [clean_data.csv]

### Problem

The dataset contained:

- Missing values in the following columns:
  [contact_no, amt_paid, customer_name, total_amt, unitPrice, receipt_no, sale_date]

- 9 duplicate rows

- Inconsistent data types:
  - sale_date → should be datetime
  - qty, unitPrice, total_amt, amt_paid → should be numeric


- Date handling:
  - sale_date cleaned as datetime inside code
  - exported as ISO string (YYYY-MM-DD)

    
- Inconsistent date formats:
  - Examples: 2025/06/13, 25-Jan-2025, Jun 10, 2025

- Inconsistent categorical values:
  - branch → ['DOWNTOWN', 'Downtown', 'NASR CITY', 'Nasr City']
  - pay_status → ['paid', 'Paid', 'PAID']
---


### Solution

Applied data cleaning using Pandas:

- Removed rows with missing values in KEY columns (receipt_no)

- Filled missing values in descriptive columns (customer_name, contact_no,sale_date)

- Removed rows with missing values in critical transactional columns (qty, unitPrice)

- Recomputed total_amt using: qty * unitprice

- Standardized data types:
  - Converted sale_date to datetime
  - Converted qty, unitPrice, total_amt, amt_paid to numeric

- Standardized categorical values:
  - branch → unified naming format
  - pay_status → normalized to consistent labels

- Removed duplicate rows based on KEY (receipt_no, item_desc)

- Applied validation rules:
  - qty, unitPrice, total_amt, amt_paid ≥ 0
  - amt_paid ≤ total_amt
  - If pay_status in ['Paid', 'Cash'] → amt_paid = total_amt

- Removed rows where qty = 0 as they represent invalid or non-transactional entries

- pay_status derived from amt_paid relative to total_amt, then aligned to ensure consistency
---
### Cleaning Summary

- Dataset cleaned and standardized for consistency and reliability

- Missing values handled based on column roles:
  - KEY → removed
  - DESC → filled using group logic
  - TRANS → removed or filled based on impact

- Duplicate records removed based on defined KEY

- Data types corrected to appropriate formats (datetime, numeric)

- Categorical values normalized to ensure consistency

- Derived column (total_amt) recalculated to ensure accuracy

- Validation rules applied to enforce data integrity

- Final dataset is clean, consistent, and ready for analysis
---

## Before vs After

### Before
- Dataset size: 338 rows × 12 columns
- Missing values across 7 columns (up to 17 missing in contact_no)
- 9 duplicate records based on KEY
- Inconsistent data types and formats
- No validation on calculated fields or value logic

### After
- Dataset size: 258 rows × 12 columns (cleaned dataset)
- No missing values remaining
- 0 duplicate records based on KEY
- All key integrity checks passed (no missing / no duplicates)
- All critical numeric fields validated (no negative values)
- total_amt fully consistent with qty × unitPrice
---

### Tools
- Python
- Pandas

---

### Deliverables
- Cleaned CSV
- Jupyter Notebook
- Cleaning Report

---

### Result

Dataset is now consistent, fully validated, and ready for analysis