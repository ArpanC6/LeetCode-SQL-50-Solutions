# 1251. Average Selling Price

**Difficulty:** Easy
**Topic:** Basic Joins / Aggregate Functions
**LeetCode:** https://leetcode.com/problems/average-selling-price/
**Solved on:** 28/10/2026
**Runtime:** 1013 ms (Beats 31.67%)
**Status:** Accepted (19/19 testcases passed)

---

## Visual Guide (One-Page Summary)

![1251 Visual Guide](./1251_Average_Selling_Price.png)

---

## Problem Statement

**Table 1:** `Prices`

| Column Name | Type |
|-------------|------|
| product_id  | int  |
| start_date  | date |
| end_date    | date |
| price       | int  |

- `(product_id, start_date, end_date)` is the primary key.
- Indicates the price of the product in a given date range.
- There are no overlapping periods for the same product.

**Table 2:** `UnitsSold`

| Column Name   | Type |
|---------------|------|
| product_id    | int  |
| purchase_date | date |
| units         | int  |

- May contain duplicate rows.
- Indicates the date, units, and product_id of each product sold.

### Task
Find the average selling price for each product.
`average_price` should be rounded to 2 decimal places.
If a product does not have any sold units, its average selling price is assumed to be 0.

---

## Real-Life Analogy

Imagine you run a supermarket. You have:
- A list of prices (which price was active on which dates).
- A list of sales (what was sold and on what date).

To find the average selling price per product:
1. Match each sale with the correct price using the **purchase date** (it must fall between `start_date` and `end_date`).
2. Compute total revenue = `units * price`.
3. Divide by total units sold.
4. If a product has no sales, set the average price to 0.

---

## Example Walkthrough

### Input: Prices
| product_id | start_date | end_date   | price |
|------------|------------|------------|-------|
| 1          | 2019-02-17 | 2019-02-28 | 5     |
| 1          | 2019-03-01 | 2019-03-22 | 20    |
| 2          | 2019-02-01 | 2019-02-20 | 15    |
| 2          | 2019-02-21 | 2019-03-31 | 30    |

### Input: UnitsSold
| product_id | purchase_date | units |
|------------|---------------|-------|
| 1          | 2019-02-25    | 100   |
| 1          | 2019-03-01    | 15    |
| 2          | 2019-02-10    | 200   |
| 2          | 2019-03-22    | 30    |

### Step 1: Match each sale to the correct price

For Product 1:
- Feb 25 -> active price is 5 (range Feb 17–28) -> revenue = 100 * 5 = 500
- Mar 01 -> active price is 20 (range Mar 1–22) -> revenue = 15 * 20 = 300

For Product 2:
- Feb 10 -> active price is 15 -> revenue = 200 * 15 = 3000
- Mar 22 -> active price is 30 -> revenue = 30 * 30 = 900

### Step 2: Compute average per product
- Product 1: (500 + 300) / (100 + 15) = 800 / 115 = 6.956... -> **6.96**
- Product 2: (3000 + 900) / (200 + 30) = 3900 / 230 = 16.956... -> **16.96**

### Output
| product_id | average_price |
|------------|---------------|
| 1          | 6.96          |
| 2          | 16.96         |

---

## Final Query

```sql
SELECT 
    p.product_id,
    IFNULL(ROUND(SUM(u.units * p.price) / SUM(u.units), 2), 0) AS average_price
FROM Prices p
LEFT JOIN UnitsSold u 
    ON p.product_id = u.product_id
    AND u.purchase_date BETWEEN p.start_date AND p.end_date
GROUP BY p.product_id;