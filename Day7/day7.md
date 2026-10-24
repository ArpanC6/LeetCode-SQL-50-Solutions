# 1068. Product Sales Analysis I

**Difficulty:** Easy
**Topic:** Basic Joins / INNER JOIN
**LeetCode:** https://leetcode.com/problems/product-sales-analysis-i/
**Solved on:** 11/10/2026
**Runtime:** 1545 ms (Beats 20.87%)
**Status:** Accepted (13/13 testcases passed)

---


## Problem Statement

**Table 1:** `Sales`

| Column Name | Type |
|-------------|------|
| sale_id     | int  |
| product_id  | int  |
| year        | int  |
| quantity    | int  |
| price       | int  |

- `(sale_id, year)` is the primary key.
- `product_id` is a foreign key to the Product table.
- Each row shows a sale of the product `product_id` in a certain year.
- Note: price is per unit.

**Table 2:** `Product`

| Column Name  | Type    |
|--------------|---------|
| product_id   | int     |
| product_name | varchar |

- `product_id` is the primary key.
- Each row indicates the product name of each product.

### Task
Report the `product_name`, `year`, and `price` for each `sale_id` in the Sales table.

Return result in any order.

---

## Understanding the Problem

I have 2 tables:
1. `Sales` — has sales info (product_id, year, price, quantity)
2. `Product` — has product names (product_id, product_name)

I need to:
1. Go through every sale in the Sales table
2. Look up its product_name from the Product table
3. Output product_name, year, and price for each sale

This is a classic **INNER JOIN** case because:
- Every sale has a matching product_id in the Product table
- No missing product_ids exist

---

## Why INNER JOIN (not LEFT JOIN)?

| JOIN Type | What It Does | Result |
|-----------|--------------|--------|
| **INNER JOIN** | Only matching rows | All sales (every sale has a product) |
| **LEFT JOIN** | All rows from left + matching right | Same result here, but not semantically needed |

The problem assumes every sale has a valid product. So INNER JOIN is the natural choice.

---

## Example Walkthrough

### Input: Sales table

| sale_id | product_id | year | quantity | price |
|---------|------------|------|----------|-------|
| 1       | 100        | 2008 | 10       | 5000  |
| 2       | 100        | 2009 | 12       | 5000  |
| 7       | 200        | 2011 | 15       | 9000  |

### Input: Product table

| product_id | product_name |
|------------|--------------|
| 100        | Nokia        |
| 200        | Apple        |
| 300        | Samsung      |

### Step 1: Match each sale with product_name

| sale_id | product_id | product_name | year | price |
|---------|------------|--------------|------|-------|
| 1       | 100        | Nokia        | 2008 | 5000  |
| 2       | 100        | Nokia        | 2009 | 5000  |
| 7       | 200        | Apple        | 2011 | 9000  |

### Output

| product_name | year | price |
|--------------|------|-------|
| Nokia        | 2008 | 5000  |
| Nokia        | 2009 | 5000  |
| Apple        | 2011 | 9000  |

**Explanation:**
- From sale_id=1, Nokia was sold for 5000 in 2008
- From sale_id=2, Nokia was sold for 5000 in 2009
- From sale_id=7, Apple was sold for 9000 in 2011

---

## Final Query

```sql
SELECT product_name, year, price
FROM Sales
JOIN Product ON Sales.product_id = Product.product_id;