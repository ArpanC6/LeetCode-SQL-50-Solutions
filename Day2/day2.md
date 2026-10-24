# 584. Find Customer Referee

**Difficulty:** Easy
**Topic:** Select / NULL Handling
**LeetCode:** https://leetcode.com/problems/find-customer-referee/
**Solved on:** [7.10.2026]

---


## Problem Statement

**Table:** `Customer`

| Column Name | Type    | Description |
|-------------|---------|-------------|
| id          | int     | Primary Key |
| name        | varchar | Customer name |
| referee_id  | int     | ID of the customer who referred them |

Each row of this table indicates the id of a customer, their name, and the id of the customer who referred them.

### Task
Find the names of the customers that are either:
1. Referred by any customer with `id != 2`
2. Not referred by any customer (i.e. `referee_id IS NULL`)

Return the result table in any order.

---

## Understanding the Conditions

### Condition 1: Referred by any customer with `id != 2`
- Look at the `referee_id` column.
- If `referee_id = 2`, that person is NOT eligible.
- If `referee_id = 1, 3, 4, ...` (any value except 2), they are eligible.

### Condition 2: Not referred by any customer
- That means `referee_id IS NULL`.
- These customers are also eligible.

### Combine the Conditions
So, we need customers where:

```sql
referee_id != 2 OR referee_id IS NULL