# 1757. Recyclable and Low Fat Products

**Difficulty:** Easy
**Topic:** Select / Basic Filtering
**LeetCode:** https://leetcode.com/problems/recyclable-and-low-fat-products/
**Solved on:** 07/10/2026

---

## Visual Guide (One-Page Summary)

![1757 Visual Guide](./1757_Recyclable_and_Low_Fat_Products.png)

---

## Problem Statement

**Table:** `Products`

| Column Name | Type |
|-------------|------|
| product_id  | int  |
| low_fats    | enum |
| recyclable  | enum |

- `product_id` is the primary key (unique value).
- `low_fats` is an ENUM of type ('Y', 'N')
  - 'Y' means the product is low fat
  - 'N' means the product is not low fat
- `recyclable` is an ENUM of type ('Y', 'N')
  - 'Y' means the product is recyclable
  - 'N' means the product is not recyclable

### Task
Find the IDs of products that are **both low fat and recyclable**.

Return the result in any order.

---

## Example

### Input: Products table

| product_id | low_fats | recyclable |
|------------|----------|------------|
| 0          | Y        | N          |
| 1          | Y        | Y          |
| 2          | N        | Y          |
| 3          | Y        | Y          |
| 4          | N        | N          |

### Output:

| product_id |
|------------|
| 1          |
| 3          |

### Explanation
- Product 0: Low fat but not recyclable -> exclude
- Product 1: Low fat and recyclable -> include
- Product 2: Not low fat -> exclude
- Product 3: Low fat and recyclable -> include
- Product 4: Not low fat -> exclude

Only products **1** and **3** satisfy both conditions.

---

## Thinking Process

### Step 1: What is the output?
We only need the `product_id`.
So we write `SELECT product_id`.

### Step 2: Which table is the data from?
From the `Products` table.
So we write `FROM Products`.

### Step 3: What are the conditions?
- Condition 1: `low_fats = 'Y'`
- Condition 2: `recyclable = 'Y'`

### Step 4: How do we combine the conditions?
Both must be true, so we use `AND`.
`AND` means both conditions must be satisfied.

### Step 5: Final Query

```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y' AND recyclable = 'Y';