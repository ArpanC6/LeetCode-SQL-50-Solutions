# 1070. Product Sales Analysis III

**Difficulty:** Medium
**Topic:** Sorting and Grouping / Subqueries / CTE
**LeetCode:** https://leetcode.com/problems/product-sales-analysis-iii/
**Solved on:** 15/11/2026
**Runtime:** 633 ms (Beats 99.63%)
**Status:** Accepted (10/10 testcases passed)

---


## Problem Statement

**Table:** `Sales`

| Column Name | Type |
|-------------|------|
| sale_id     | int  |
| product_id  | int  |
| year        | int  |
| quantity    | int  |
| price       | int  |

- `(sale_id, year)` is the primary key.
- Each row records a sale of a product in a given year.
- A product may have multiple sales entries in the same year.
- Note that `price` is per-unit.

### Task
Find all sales that occurred in the **first year** each product was sold.

For each `product_id`, identify the earliest year it appears in the Sales table. Return all sales entries for that product in that year.

Return columns: `product_id`, `first_year`, `quantity`, `price`.

---

## Real-Life Analogy

Imagine you manage a store. You want to see the very first sales of each product when it was newly launched.

- Product 100 was first sold in 2008.
- Product 200 was first sold in 2011.

You need to show the exact quantity and price for those first-year sales.

---

## Example Walkthrough

### Input: Sales table
| sale_id | product_id | year | quantity | price |
|---------|------------|------|----------|-------|
| 1       | 100        | 2008 | 10       | 5000  |
| 2       | 100        | 2009 | 12       | 5000  |
| 7       | 200        | 2011 | 15       | 9000  |

### Step 1: Find the first year per product
- Product 100: `MIN(year) = 2008`
- Product 200: `MIN(year) = 2011`

### Step 2: Filter Sales to only those first-year rows
- Row for product 100 in 2008 (sale_id 1).
- Row for product 200 in 2011 (sale_id 7).

### Output
| product_id | first_year | quantity | price |
|------------|------------|----------|-------|
| 100        | 2008       | 10       | 5000  |
| 200        | 2011       | 15       | 9000  |

---

## Final Query (Approach 1: Using Subquery/JOIN)

```sql
SELECT 
    s.product_id,
    s.year AS first_year,
    s.quantity,
    s.price
FROM Sales s
JOIN (
    SELECT product_id, MIN(year) AS min_year
    FROM Sales
    GROUP BY product_id
) f 
ON s.product_id = f.product_id 
AND s.year = f.min_year;