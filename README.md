# Vendor Reconciliation System
### Automated Billing Report using Fuzzy Matching | Python

## Business Problem
A large corporation outsources work to 10 third-party vendors. Employee 
check-in and check-out data was recorded internally, but vendor names 
contained typos and inconsistencies that made it impossible to reliably 
match internal records to the correct vendor.

This caused significant discrepancies between what the corporation 
calculated as owed and what vendors were actually billing — creating 
financial risk and manual reconciliation overhead.

## Why Excel Wasn't Enough
Traditional tools like Excel have no reliable way to handle fuzzy text 
matching at scale. A name like "Soluciones Tech S.A." and "Soluciones 
Tec SA" would be treated as completely different entities, making 
automated reconciliation impossible.

## The Solution
I built a Python pipeline that:
1. Loads internal employee records and the official vendor list
2. Uses **TheFuzz** library to calculate similarity scores between 
   vendor name variants
3. Identifies the correct vendor match for each record above a 
   confidence threshold
4. Calculates total hours worked per vendor based on check-in/check-out 
   timestamps
5. Computes the correct payment owed to each of the 10 vendors
6. Automatically generates a PDF report (`reporte_ventas.pdf`) with 
   tables and charts

## Tools & Libraries Used
| Library | Purpose |
|---------|---------|
| pandas | Data loading and manipulation |
| thefuzz | Fuzzy string matching |
| python-Levenshtein | Accelerates fuzzy matching |
| matplotlib | Charts and visualizations |
| fpdf2 | Automated PDF report generation |
| datetime | Timestamp calculations |

## Key Technical Decisions
- Used `token_sort_ratio` from TheFuzz for more reliable matching 
  regardless of word order
- Set a confidence threshold to flag low-confidence matches for manual 
  review instead of silently misclassifying them
- Automated the full pipeline from raw data to PDF report with a 
  single script execution

## Handling False Positives
One of the key challenges in fuzzy matching is balancing precision vs. recall. 
A threshold that is too low (e.g. 30) causes false positives — records that 
match incorrectly to the wrong vendor, silently generating billing errors that 
are harder to detect than an unmatched record.

A false positive is more dangerous than a no-match: a no-match flags a problem 
for manual review, while a false positive creates an incorrect payment that may 
go unnoticed.

After testing, a threshold of **45** was selected as the optimal balance for 
this dataset — low enough to catch legitimate name variations and typos, high 
enough to avoid incorrect matches. Records below the threshold are explicitly 
flagged as `"NO MATCH - Manual Review Required"`and added to a special table rather than force-matched.

## Output
The script automatically generates `reporte_ventas.pdf` containing:
- Matched vendor list
- Total payment owed per vendor
- Summary charts

## Screenshots
<img width="792" height="573" alt="image" src="https://github.com/user-attachments/assets/c7dacbaa-b9e4-4b62-b3b8-f049811d9d40" />

<img width="790" height="858" alt="image" src="https://github.com/user-attachments/assets/5cd49d5f-538b-4888-83bd-3bc429cb2494" />

