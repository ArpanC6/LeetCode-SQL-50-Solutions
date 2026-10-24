# 1757. Recyclable and Low Fat Products

**Difficulty:** Easy
**Topic:** Select / Basic Filtering
**LeetCode:** https://leetcode.com/problems/recyclable-and-low-fat-products/
**Solved on:** [7.10.2026]

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
  - 'Y' means product is low fat
  - 'N' means product is not low fat
- `recyclable` is an ENUM of type ('Y', 'N')
  - 'Y' means product is recyclable
  - 'N' means product is not recyclable

### Task
Find the IDs of products that are both low fat and recyclable.

Return result in any order.

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
- Product 0: low fat but not recyclable -> exclude
- Product 1: low fat and recyclable -> include
- Product 2: not low fat -> exclude
- Product 3: low fat and recyclable -> include
- Product 4: not low fat -> exclude

Only products 1 and 3 satisfy both conditions.

---

## Thinking Process

### Step 1: Output ki chai?
Amake shudhu `product_id` lagbe.
Tai `SELECT product_id` likhbo.

### Step 2: Data kon table theke?
`Products` table theke.
Tai `FROM Products` likhbo.

### Step 3: Ki condition?
- Condition 1: `low_fats = 'Y'`
- Condition 2: `recyclable = 'Y'`

### Step 4: Condition gulo kivabe jukto korbo?
Duitai true hote hobe, tai `AND` use korbo.
`AND` mane: duita condition e true hote hobe.

### Step 5: Puro query ta

```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y' AND recyclable = 'Y';