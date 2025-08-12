# Data Dictionary – Online Retail

| Column       | Type    | Missing % | Example        | Description                                  | Cleaning Notes                     |
|--------------|---------|-----------|----------------|----------------------------------------------|------------------------------------|
| InvoiceNo    | string  |           | 536365         | Invoice number                               | Remove non-numeric, mark returns   |
| StockCode    | string  |           | 85123A         | Item code                                    | Trim spaces                        |
| Description  | string  |           | WHITE HANGING… | Item description                             | Strip HTML/whitespaces             |
| Quantity     | int     |           | 6              | Quantity purchased                           | Handle negatives (returns)         |
| InvoiceDate  | datetime|           | 2010-12-01 …   | Invoice timestamp                            | Parse timezone, month key          |
| UnitPrice    | float   |           | 2.55           | Unit price                                   | Non-negative, currency             |
| CustomerID   | string  |           | 17850          | Customer identifier                          | Deduplicate, missing strategy      |
| Country      | string  |           | United Kingdom | Country                                      | Normalize country names            |

## Planned Cleaning
- Remove duplicates by (InvoiceNo, StockCode, InvoiceDate).
- Negative `Quantity` → mark as returns; consider excluding from RFM or treat separately.
- Drop rows with missing `CustomerID` for customer-level modeling; keep for sales EDA.
- Create `Revenue = Quantity * UnitPrice`; month/year keys for cohort analysis.
