# 1193. Monthly Transactions I

**Difficulty:** Medium
**Topic:** Basic Aggregate Functions / Date Formatting / Conditional Aggregation
**LeetCode:** https://leetcode.com/problems/monthly-transactions-i/
**Solved on:** 05/11/2026
**Runtime:** 637 ms (Beats 56.82%)
**Status:** Accepted (16/16 testcases passed)

---


## Problem Statement

**Table:** `Transactions`

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| country     | varchar |
| state       | enum    |
| amount      | int     |
| trans_date  | date    |

- `id` is the primary key.
- `state` is an ENUM of type `["approved", "declined"]`.

### Task
Write an SQL query to find for each month and country:
1. The number of transactions (`trans_count`) and their total amount (`trans_total_amount`).
2. The number of approved transactions (`approved_count`) and their total amount (`approved_total_amount`).

Return the result table in any order.

---

## Real-Life Analogy

Imagine you are a bank manager. You have a list of transactions.
- Each transaction has a country, a status (approved/declined), an amount, and a date.
- You want a monthly report by country:
  - How many transactions occurred?
  - How much money was moved in total?
  - How many were approved?
  - How much money was in approved transactions only?

This requires grouping by **month (from date)** and **country**, and computing four metrics.

---

## Example Walkthrough

### Input: Transactions table
| id  | country | state    | amount | trans_date |
|-----|---------|----------|--------|------------|
| 121 | US      | approved | 1000   | 2018-12-18 |
| 122 | US      | declined | 2000   | 2018-12-19 |
| 123 | US      | approved | 2000   | 2019-01-01 |
| 124 | DE      | approved | 2000   | 2019-01-07 |

### Step 1: Extract Month (`YYYY-MM`)
- 2018-12-18 -> 2018-12
- 2018-12-19 -> 2018-12
- 2019-01-01 -> 2019-01
- 2019-01-07 -> 2019-01

### Step 2: Group by Month and Country
- Group 1: 2018-12, US (2 transactions)
- Group 2: 2019-01, US (1 transaction)
- Group 3: 2019-01, DE (1 transaction)

### Step 3: Compute Metrics

| month   | country | trans_count | approved_count | trans_total_amount | approved_total_amount |
|---------|---------|-------------|----------------|--------------------|-----------------------|
| 2018-12 | US      | 2           | 1              | 3000               | 1000                  |
| 2019-01 | US      | 1           | 1              | 2000               | 2000                  |
| 2019-01 | DE      | 1           | 1              | 2000               | 2000                  |

---

## Final Query

```sql
SELECT 
    DATE_FORMAT(trans_date, '%Y-%m') AS month,
    country,
    COUNT(*) AS trans_count,
    SUM(state = 'approved') AS approved_count,
    SUM(amount) AS trans_total_amount,
    SUM(CASE WHEN state = 'approved' THEN amount ELSE 0 END) AS approved_total_amount
FROM Transactions
GROUP BY DATE_FORMAT(trans_date, '%Y-%m'), country;