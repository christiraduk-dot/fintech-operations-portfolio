# FinTech Operations: Automated Payment Reconciliation Engine

## 📌 Project Overview
In financial operations, manual reconciliation between internal transaction logs and bank settlement reports is slow and prone to human error. This project demonstrates a **SQL-based automated engine** designed to identify missing settlements, payout discrepancies, and data integrity issues.

## 🛠 Tech Stack
* **Language:** SQL (SQLite)
* **Tools:** DB Browser for SQLite, Excel
* **Concepts:** Data Normalization, Type Casting, Joins, and Case Logic.

## 🏗 Database Architecture
The project utilizes a relational structure comparing two primary data sources:
1. `Transactions`: Internal record of sales/payments initiated.
2. `Settlements`: External bank/processor reports of successfully cleared funds.

## 💻 Key SQL Implementation: Reconciliation Logic
Using a `LEFT JOIN`, I engineered a query to identify transactions that were recorded internally but never reached the bank (missing payouts), and categorized them by status.

```sql
SELECT 
  t."Transaction ID", 
  t."Amount" AS transaction_amount, 
  s."Settled_Amount" AS settled_amount,
  CASE
    WHEN s."Settled_Amount" IS NULL THEN 'Missing'
    WHEN t."Amount" = s."Settled_Amount" THEN 'OK'
    ELSE 'Mismatch'
  END AS match_status
FROM "transactions" AS t
LEFT JOIN "settlements" AS s 
  ON t."Transaction ID" = s."Transaction_ID";

##Business Impact
Efficiency: Automated the cross-referencing of transaction data, replacing manual Excel lookups.

Risk Mitigation: Identified high-risk discrepancies (Missing Settlements) that represent potential financial loss.

Scalability: Built a reusable logic that can be applied to large-scale B2B portfolios (e.g., SAP/Oracle exports).
