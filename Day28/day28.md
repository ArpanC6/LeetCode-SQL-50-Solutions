# 619. Biggest Single Number

**Difficulty:** Easy
**Topic:** Sorting and Grouping / Subqueries / Aggregation
**LeetCode:** https://leetcode.com/problems/biggest-single-number/
**Solved on:** 23/11/2026
**Runtime:** 471 ms (Beats 60.27%)
**Status:** Accepted (18/18 testcases passed)

---

## Problem Statement

**Table:** `MyNumbers`

| Column Name | Type |
|-------------|------|
| num         | int  |

- This table may contain duplicates (there is no primary key).
- Each row of this table contains an integer.

### Task
A **single number** is a number that appeared **only once** in the `MyNumbers` table.

Find the **largest single number**. If there is no single number, report `null`.

---

## Real-Life Analogy (Card Piles)

You have cards with numbers written on them: `8, 8, 3, 3, 1, 4, 5, 6`

1. **Make piles** of the same number (`GROUP BY num`):
   - Pile 8: [8] [8]
   - Pile 3: [3] [3]
   - Pile 1: [1]
   - Pile 4: [4]
   - Pile 5: [5]
   - Pile 6: [6]
2. **Count cards in each pile** (`COUNT(*)`): 8 -> 2, 3 -> 2, 1 -> 1, 4 -> 1, 5 -> 1, 6 -> 1
3. **Keep only piles with exactly 1 card** (`HAVING COUNT(*) = 1`): 1, 4, 5, 6
4. **Pick the biggest** of the remaining (`MAX(num)`): **6**

---

## Example Walkthrough

### Example 1

| num |
|-----|
| 8 |
| 8 |
| 3 |
| 3 |
| 1 |
| 4 |
| 5 |
| 6 |

Single numbers: `1, 4, 5, 6` -> largest is `6`.

| num |
|-----|
| 6   |

### Example 2

| num |
|-----|
| 8 |
| 8 |
| 7 |
| 7 |
| 3 |
| 3 |
| 3 |

No number appears exactly once -> inner query is empty -> `MAX` of an empty set is `NULL`.

| num  |
|------|
| null |

---

## Step-by-Step Build

**Step 1: See all data**
```sql
SELECT num FROM MyNumbers;
```

**Step 2: Group same numbers**
```sql
SELECT num FROM MyNumbers GROUP BY num;
```

**Step 3: Count each group**
```sql
SELECT num, COUNT(*) AS cnt FROM MyNumbers GROUP BY num;
```

**Step 4: Keep only count = 1**
```sql
SELECT num
FROM MyNumbers
GROUP BY num
HAVING COUNT(*) = 1;
```

**Step 5: Take the maximum of that result (wrap in a subquery)**

---

## Final Query

```sql
SELECT MAX(num) AS num
FROM (
    SELECT num
    FROM MyNumbers
    GROUP BY num
    HAVING COUNT(*) = 1
) AS t;
```

---

## Key Concepts

- `GROUP BY num` only bundles same values together. It does not add or multiply anything.
- `COUNT(*)` counts rows in each bundle.
- `HAVING` filters **after** grouping; `WHERE` filters **before** grouping. So `WHERE COUNT(*) = 1` gives an error.
- SQL execution order: `FROM` -> `GROUP BY` -> `COUNT` -> `HAVING` -> `SELECT`.
- `MAX()` on an empty set returns `NULL`, so no special handling is needed for the "no single number" case.
- In MySQL, a subquery in `FROM` **must have an alias** (`AS t`).

---

## Mistakes / Notes

- Confusion: `HAVING COUNT(*) = 1` keeps piles with count 1 and **throws away** piles with count 2 or more.
- When pasting a new solution in LeetCode, clear the editor first (`Ctrl + A`, `Delete`) so old code does not mix in.