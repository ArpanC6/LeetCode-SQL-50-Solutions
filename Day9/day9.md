# 197. Rising Temperature

**Difficulty:** Easy
**Topic:** Basic Joins / SELF JOIN
**LeetCode:** https://leetcode.com/problems/rising-temperature/
**Solved on:** 14/10/2026
**Runtime:** 866 ms (Beats 6.05%)
**Status:** Accepted (15/15 testcases passed)

---


## Problem Statement

**Table:** `Weather`

| Column Name | Type |
|-------------|------|
| id          | int  |
| recordDate  | date |
| temperature | int  |

- `id` is unique.
- There are no different rows with the same `recordDate`.
- This table contains info about the temperature on a certain day.

### Task
Find all dates' **id** with **higher temperatures compared to its previous dates (yesterday)**.

Return result in any order.

---

## Real-Life Analogy

Imagine you are a weather station manager. You have ONE register that has temperature for each day.

**Goal:** Find days where the temperature was **higher than the previous day**.

- Jan 1 → 10°
- Jan 2 → 25° → higher than Jan 1 (10) → YES
- Jan 3 → 20° → not higher than Jan 2 (25) → NO
- Jan 4 → 30° → higher than Jan 3 (20) → YES

So output: id = 2 and id = 4.

This requires comparing **a row with another row in the same table** → **SELF JOIN**.

---

## Understanding the Problem

We have only **ONE table**. We need to:
1. Compare each row with the previous day's row
2. Check if today's temperature > yesterday's temperature
3. Return the id of the current day

Key insight: There is no second table — we must join the table with itself.

---

## What is SELF JOIN?

**SELF JOIN** means: using the **same table twice** with **two different aliases**.

```sql
FROM Weather w1, Weather w2