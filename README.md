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

## Output
The script automatically generates `reporte_ventas.pdf` containing:
- Matched vendor list with confidence scores
- Hours worked per vendor
- Total payment owed per vendor
- Summary charts

## Screenshots
<img width="987" height="710" alt="image" src="https://github.com/user-attachments/assets/ac7c6990-801b-4828-8641-7cce4d8172a9" />

<img width="792" height="851" alt="image" src="https://github.com/user-attachments/assets/0e070793-c3e0-4968-af6a-d63eb07cef23" />

