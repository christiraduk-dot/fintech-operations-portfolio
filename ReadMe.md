# Payments Reconciliation & Settlement Analysis

## Overview
This project simulates a FinTech operations reconciliation process by matching payment transactions against settlement records to identify missing and mismatched payouts.

## Objective
Ensure settlement accuracy by detecting:
- Missing settlements
- Amount mismatches
- Successfully settled transactions

## Data
- transactions.csv: Source payment transactions
- settlements.csv: Settlement records from a payment processor

## Methodology
- Imported transactional data into SQLite
- Used SQL LEFT JOINs to reconcile transactions with settlements
- Applied CASE logic to classify settlement status (OK / Missing / Mismatch)
- Created a reconciliation view for reusable analysis
- Generated summary metrics to assess settlement health

## Tools
- SQL (SQLite)
- DB Browser for SQLite
- Spreadsheet preprocessing (Excel / Google Sheets)

## Key Outcomes
- Identified settlement exceptions and discrepancies
- Built a reusable reconciliation view
- Produced summary counts for operational monitoring

