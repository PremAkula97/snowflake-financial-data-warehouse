# Snowflake Financial Data Warehouse & ELT Pipeline

A hands-on financial data engineering project built using Snowflake SQL, demonstrating data warehousing, ELT transformations, data validation, and financial reconciliation.

## Project Overview

This project simulates a financial transaction processing pipeline using synthetic banking data.

Raw transactions are loaded into Snowflake, validated, separated into accepted and rejected records, and transformed into analytics-ready tables.

The pipeline also generates daily financial summaries and performs source-to-target reconciliation.

## Technologies Used

- Snowflake
- SQL
- Data Warehousing
- ELT (Extract, Load, Transform)
- Data Mapping and Transformation
- Data Quality Validation
- Financial Reconciliation
- Git and GitHub

## Data Pipeline Architecture

```text
Synthetic Financial Transactions
              |
              v
    RAW.TRANSACTIONS
              |
       Data Validation
          /       \
         v         v
  Valid Records  Rejected Records
         |         |
         v         v
 CLEAN_TRANSACTIONS  REJECTED_TRANSACTIONS
         |
         v
   DAILY_SUMMARY
         |
         v
 Financial Reconciliation
```

## Database Structure

**Database:** FINANCIAL_WAREHOUSE

**RAW schema**
- TRANSACTIONS: Original financial transaction records.

**ANALYTICS schema**
- CLEAN_TRANSACTIONS: Validated transactions with signed cash flow amounts.
- REJECTED_TRANSACTIONS: Invalid records with rejection reasons.
- DAILY_SUMMARY: Aggregated daily deposits, withdrawals, and net cash flow.

## Data Quality Rules

Transactions are rejected if:

- Transaction ID is missing.
- Customer ID is missing.
- Transaction date is missing.
- Transaction amount is missing or nonpositive.
- Transaction type is not DEPOSIT or WITHDRAWAL.

## Execution Results

| Metric | Result |
|---|---:|
| Source records | 12 |
| Valid records | 10 |
| Rejected records | 2 |
| Daily summary records | 5 |
| Source-to-target count reconciliation | PASSED |

## Financial Reconciliation

The pipeline compares the net cash flow calculated from individual valid transactions against the aggregated daily summaries.

Expected results for the provided synthetic dataset:

| Metric | Amount |
|---|---:|
| Total deposits | $17,000 |
| Total withdrawals | $5,000 |
| Net cash flow | $12,000 |
| Detail-to-summary reconciliation | PASSED |

## SQL Scripts

Run these scripts in order:

1. `sql/01_setup.sql` — Creates the database, schemas, and tables.
2. `sql/02_load_data.sql` — Inserts synthetic transaction records.
3. `sql/03_transform.sql` — Validates, transforms, and aggregates transactions.
4. `sql/04_analysis.sql` — Runs financial analysis and reconciliation queries.

Run the complete scripts in a Snowflake SQL worksheet. The transformation script clears its target tables before rebuilding them.

**Note:** The load script uses INSERT statements. Avoid running it repeatedly without clearing the raw table, as this will duplicate source records.

## Future Improvements

- Automate ingestion using Snowpipe.
- Add incremental ELT processing with Snowflake Streams and Tasks.
- Introduce dimensional data models.
- Integrate dashboards for financial reporting.
- Implement automated data quality tests.

## Author

Prem Sai Akula

GitHub: https://github.com/PremAkula97

*All financial transactions are synthetic and intended for educational purposes.*