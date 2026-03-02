# ETL - Online Retail Sales

ETL pipeline for online retail sales data built with Google Apps Script and Google Sheets, with no paid tools required.

## Stack

- **Google Sheets** — raw data storage and report output
- **Google Apps Script** — pipeline processing (Extract, Transform, Load)

## Pipeline structure

```
CSV (raw data)
     ↓
Extract   → reads data from the first Sheets tab
Transform → cleans, validates and enriches records
Load      → generates aggregated report tabs
```

## Transformations applied

- Removal of empty rows and rows without an invoice
- Deduplication by `Invoice + StockCode`
- Returns filtered out (negative quantity or price)
- `Total = Quantity × Price` calculation
- `YearMonth` extraction from `InvoiceDate`

## Output

| Sheet | Description |
|-------|-------------|
| `Relatorio_Produto` | Total sold per product, sorted by revenue |
| `Relatorio_Pais` | Total sold per country |
| `Relatorio_Mensal` | Monthly sales evolution |

## Dataset

[Online Retail Dataset - UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/Online+Retail)

Columns: `Invoice`, `StockCode`, `Description`, `Quantity`, `InvoiceDate`, `Price`, `Customer ID`, `Country`

## How to use

1. Upload the CSV to Google Sheets
2. Open **Extensions → Apps Script**
3. Paste the contents of `etl.gs` and save
4. Select the `runETL` function and click **Run**
5. Authorize the required permissions when prompted
6. Reports will be automatically created as new tabs
