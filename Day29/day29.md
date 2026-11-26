# 1045. Customers Who Bought All Products

**Difficulty:** Medium
**Topic:** Sorting and Grouping / Aggregation
**LeetCode:** https://leetcode.com/problems/customers-who-bought-all-products/
**Solved on:** 26/11/2026
**Runtime:** (fill in from your submission) ms (Beats __%)
**Status:** Accepted (__/__ testcases passed)

---

## Problem Statement

**Table:** `Customer`

| Column Name | Type |
|-------------|------|
| customer_id | int  |
| product_key | int  |

- This table may contain duplicate rows.
- `customer_id` is not NULL.
- `product_key` is a foreign key (reference column) to the `Product` table.

**Table:** `Product`

| Column Name | Type |
|-------------|------|
| product_key | int  |

- `product_key` is the primary key (column with unique values) for this table.

### Task
Write a solution to report the `customer_id` of every customer who bought **all** the products in the `Product` table.

Return the result table in **any order**.

---

## Real-Life Analogy: Sticker Album

An album has a fixed number of slots. This is the **Product table**.
Each friend has bought some stickers. This is the **Customer table**.

Question: **whose album is completely filled?**

In the example the album has 2 slots (5 and 6):

```
Friend 1:  5, 6     -> 2 different stickers -> album complete
Friend 2:  6        -> 1 different sticker  -> album incomplete
Friend 3:  5, 6     -> 2 different stickers -> album complete
```

Answer: Friends 1 and 3.

---

## Example Walkthrough

### Input

**Customer table**

| customer_id | product_key |
|-------------|-------------|
| 1           | 5           |
| 2           | 6           |
| 3           | 5           |
| 3           | 6           |
| 1           | 6           |

**Product table**

| product_key |
|-------------|
| 5           |
| 6           |

### Output

| customer_id |
|-------------|
| 1           |
| 3           |

**Explanation:** The store has 2 products (5 and 6). Customers 1 and 3 bought both. Customer 2 bought only 6.

---

## Core Idea

> If a customer's **number of distinct products** equals the **total number of products** in the Product table, that customer bought everything.

---

## Step-by-Step Build

**Step 1: Group the rows by customer**

```sql
GROUP BY customer_id
```

**Step 2: Count the distinct products in each group**

```sql
COUNT(DISTINCT product_key)
```

| customer_id | COUNT(DISTINCT product_key) |
|-------------|-----------------------------|
| 1           | 2                           |
| 2           | 1                           |
| 3           | 2                           |

**Step 3: Count the total number of products in the store**

```sql
(SELECT COUNT(*) FROM Product)
```

In the example this returns 2.

**Step 4: Keep only the groups where the two numbers are equal (HAVING)**

```sql
HAVING COUNT(DISTINCT product_key) = (SELECT COUNT(*) FROM Product)
```

| customer_id | distinct products | total products | Equal? |
|-------------|-------------------|----------------|--------|
| 1           | 2                 | 2              | keep   |
| 2           | 1                 | 2              | drop   |
| 3           | 2                 | 2              | keep   |

---

## Final Query

```sql
SELECT customer_id
FROM Customer
GROUP BY customer_id
HAVING COUNT(DISTINCT product_key) = (SELECT COUNT(*) FROM Product);
```

---

## SQL Execution Order (for this query)

1. `FROM Customer`: take the Customer table
2. `GROUP BY customer_id`: build one group per customer
3. `COUNT(DISTINCT product_key)`: count distinct products in each group
4. `HAVING ... = (SELECT COUNT(*) FROM Product)`: keep only groups whose count equals the total
5. `SELECT customer_id`: show the remaining customer ids

---

## Key Concepts

| Concept | Meaning |
|---------|---------|
| `GROUP BY customer_id` | Puts rows of the same customer into one group. It does not add or count anything by itself |
| `COUNT(DISTINCT col)` | Counts each value once, no matter how many times it repeats |
| `HAVING` | Filters groups after grouping and counting are done |
| `WHERE` | Filters rows before grouping, so `WHERE COUNT(...)` is not allowed |
| Subquery in `HAVING` | Fetches the total product count from the Product table |

---

## Test Yourself

Product table: 1, 2, 3. Customer table:

| customer_id | product_key |
|-------------|-------------|
| 10          | 1           |
| 10          | 2           |
| 10          | 3           |
| 20          | 1           |
| 20          | 1           |
| 20          | 2           |
| 30          | 1           |
| 30          | 2           |
| 30          | 3           |
| 30          | 3           |

- Total products = 3
- Customer 10 -> 3 distinct, Customer 20 -> 2 distinct (1 appears twice but counts once), Customer 30 -> 3 distinct
- Answer: **10, 30**

---

## Common Mistakes

- Forgetting `DISTINCT`: duplicate rows get counted. Customer 20 (1, 1, 2) would count as 3 and wrongly match the total of 3.
- Writing `WHERE COUNT(...) = ...`: this is an error. Filtering on a count needs `HAVING`.
- Using `COUNT(*)` instead of `COUNT(DISTINCT product_key)`: it counts duplicate rows too.
- Hard-coding the total (for example `= 2`): the total must come from `(SELECT COUNT(*) FROM Product)` so it works for any Product table.

---

## Key Takeaways

- When duplicates are possible, use `COUNT(DISTINCT ...)`.
- For "bought all / has every" problems, compare each group's distinct count with the total count in `HAVING`.
- On the left of the `=` in `HAVING` is what the customer has; on the right is what the store has.