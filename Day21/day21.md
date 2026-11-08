# 1174. Immediate Food Delivery II

**Difficulty:** Medium
**Topic:** Basic Aggregate Functions / Subqueries / Window Functions
**LeetCode:** https://leetcode.com/problems/immediate-food-delivery-ii/
**Solved on:** 08/11/2026
**Runtime:** 728 ms (Beats 50.36%)
**Status:** Accepted (23/23 testcases passed)

---


## Problem Statement

**Table:** `Delivery`

| Column Name                 | Type |
|-----------------------------|------|
| delivery_id                 | int  |
| customer_id                 | int  |
| order_date                  | date |
| customer_pref_delivery_date | date |

- `delivery_id` is the primary key.
- If `order_date == customer_pref_delivery_date`, the order is **immediate**.
- Otherwise, it is **scheduled**.
- The **first order** is the one with the earliest `order_date` per customer.

### Task
Find the **percentage of immediate orders** among the **first orders** of all customers, rounded to 2 decimal places.

---

## Real-Life Analogy

Imagine you manage a food delivery app.
- Some customers want food immediately (same day).
- Others schedule it for a future date.

You only care about each customer's **very first order**.
Among those first orders, what percentage were immediate?

---

## Example Walkthrough

### Input: Delivery table
| delivery_id | customer_id | order_date | customer_pref_delivery_date |
|-------------|-------------|------------|-----------------------------|
| 1           | 1           | 2019-08-01 | 2019-08-02                  |
| 2           | 2           | 2019-08-02 | 2019-08-02                  |
| 3           | 1           | 2019-08-11 | 2019-08-12                  |
| 4           | 3           | 2019-08-24 | 2019-08-24                  |
| 5           | 3           | 2019-08-21 | 2019-08-22                  |
| 6           | 2           | 2019-08-11 | 2019-08-13                  |
| 7           | 4           | 2019-08-09 | 2019-08-09                  |

### Step 1: Find each customer's first order
- Customer 1: delivery_id 1 (order_date 2019-08-01)
- Customer 2: delivery_id 2 (order_date 2019-08-02)
- Customer 3: delivery_id 5 (order_date 2019-08-21)
- Customer 4: delivery_id 7 (order_date 2019-08-09)

### Step 2: Check if each is immediate (order_date == pref_delivery_date)
- Customer 1: NO (2019-08-01 != 2019-08-02) → scheduled
- Customer 2: YES (2019-08-02 == 2019-08-02) → immediate
- Customer 3: NO (2019-08-21 != 2019-08-22) → scheduled
- Customer 4: YES (2019-08-09 == 2019-08-09) → immediate

### Step 3: Compute percentage
- 2 immediate out of 4 first orders = 50.00%

### Output
| immediate_percentage |
|----------------------|
| 50.00                |

---

## Final Query (Approach 1: Using IN Subquery)

```sql
SELECT
    ROUND(SUM(order_date = customer_pref_delivery_date) / COUNT(*) * 100, 2) AS immediate_percentage
FROM Delivery
WHERE (customer_id, order_date) IN (
    SELECT customer_id, MIN(order_date)
    FROM Delivery
    GROUP BY customer_id
);