# 1581. Customer Who Visited but Did Not Make Any Transactions

**Difficulty:** Easy
**Topic:** Basic Joins / LEFT JOIN / Subquery
**LeetCode:** https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/
**Solved on:** 11/10/2026
**Runtime:** 1499 ms (Beats 51.49%)
**Status:** Accepted (29/29 testcases passed)

---

## Problem Statement

**Table 1:** `Visits`

| Column Name | Type |
|-------------|------|
| visit_id    | int  |
| customer_id | int  |

- `visit_id` is unique.
- Each row contains info about customers who visited the mall.

**Table 2:** `Transactions`

| Column Name    | Type |
|----------------|------|
| transaction_id | int  |
| visit_id       | int  |
| amount         | int  |

- `transaction_id` is unique.
- Each row contains info about transactions made during a visit.

### Task
Find the IDs of users who visited **without making any transactions** and the **number of times** they made these types of visits.

Return result in any order.

---

## Real-Life Analogy

Imagine you are the manager of a mall. You have 2 registers:

**Register 1 — Visitors Register (Visits table):**
- Contains all visits to the mall
- 7 visits in total

**Register 2 — Transactions Register (Transactions table):**
- Contains all purchases made during visits
- Only 5 transactions

**What do you want to do?**
- Find customers who visited but did NOT purchase anything
- Count how many such "no-purchase visits" each customer made

This task in SQL is done with **LEFT JOIN + IS NULL** (or **NOT IN subquery**).

---

## Understanding the Problem

We have 2 tables:
1. `Visits` — all visits (7 visits)
2. `Transactions` — only visits with transactions (5 transactions)

We need to find:
1. Visits that have **no matching transaction** (using LEFT JOIN + IS NULL or NOT IN)
2. Group by customer_id and count

Key challenge:
- We need visits where the **transaction does NOT exist**
- Alice, Bob will not appear (they made transactions)
- We want the "missing" visits

---

## Why LEFT JOIN (not INNER JOIN)?

| JOIN Type | What It Does | Result |
|-----------|--------------|--------|
| **INNER JOIN** | Only matching rows | Only visits WITH transactions |
| **LEFT JOIN** | All rows from left + matching right | All visits, NULL if no transaction |

The problem says: **"visited without making any transactions"** — we need visits **without** transactions.

So we use **LEFT JOIN + WHERE ... IS NULL**.

---

## Example Walkthrough

### Input: Visits table

| visit_id | customer_id |
|----------|-------------|
| 1        | 23          |
| 2        | 9           |
| 4        | 30          |
| 5        | 54          |
| 6        | 96          |
| 7        | 54          |
| 8        | 54          |

### Input: Transactions table

| transaction_id | visit_id | amount |
|----------------|----------|--------|
| 2              | 5        | 310    |
| 3              | 5        | 300    |
| 9              | 5        | 200    |
| 12             | 1        | 910    |
| 13             | 2        | 970    |

### Step 1: Check each visit — does a transaction exist?

| visit_id | customer_id | Transaction exists? |
|----------|-------------|---------------------|
| 1        | 23          | YES                 |
| 2        | 9           | YES                 |
| 4        | 30          | NO                  |
| 5        | 54          | YES                 |
| 6        | 96          | NO                  |
| 7        | 54          | NO                  |
| 8        | 54          | NO                  |

### Step 2: Keep only visits WITHOUT transactions

| visit_id | customer_id |
|----------|-------------|
| 4        | 30          |
| 6        | 96          |
| 7        | 54          |
| 8        | 54          |

### Step 3: Group by customer_id and count

| customer_id | count_no_trans |
|-------------|----------------|
| 30          | 1              |
| 96          | 1              |
| 54          | 2              |

### Output

| customer_id | count_no_trans |
|-------------|----------------|
| 30          | 1              |
| 96          | 1              |
| 54          | 2              |

---

## Final Query (Approach 1: LEFT JOIN + IS NULL)

```sql
SELECT customer_id, COUNT(*) AS count_no_trans
FROM Visits
LEFT JOIN Transactions 
    ON Visits.visit_id = Transactions.visit_id
WHERE Transactions.visit_id IS NULL
GROUP BY customer_id;