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
    t.transaction_id,
    t.amount AS recorded_amount,
    s.settled_amount,
    COALESCE(s.settled_amount, 0) - t.amount AS discrepancy,
    CASE 
        WHEN s.transaction_id IS NULL THEN 'Missing Settlement'
        WHEN s.settled_amount != t.amount THEN 'Amount Mismatch'
        ELSE 'Reconciled'
    END AS status
FROM Transactions t
LEFT JOIN Settlements s ON t.transaction_id = s.transaction_id
WHERE status != 'Reconciled';

##Business Impact
Efficiency: Automated the cross-referencing of transaction data, replacing manual Excel lookups.

Risk Mitigation: Identified high-risk discrepancies (Missing Settlements) that represent potential financial loss.

Scalability: Built a reusable logic that can be applied to large-scale B2B portfolios (e.g., SAP/Oracle exports).
