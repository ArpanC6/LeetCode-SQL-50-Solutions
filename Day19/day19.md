# 1211. Queries Quality and Percentage

**Difficulty:** Easy
**Topic:** Basic Aggregate Functions / CASE WHEN
**LeetCode:** https://leetcode.com/problems/queries-quality-and-percentage/
**Solved on:** 04/11/2026
**Runtime:** 484 ms (Beats 24.02%)
**Status:** Accepted (14/14 testcases passed)

---

## Problem Statement

**Table:** `Queries`

| Column Name | Type    |
|-------------|---------|
| query_name  | varchar |
| result      | varchar |
| position    | int     |
| rating      | int     |

- This table may contain duplicate rows.
- `position` has a value from 1 to 500.
- `rating` has a value from 1 to 5.
- A query with rating less than 3 is a poor query.

### Task
We define:
- **Query Quality:** The average of the ratio between query rating and its position.
- **Poor Query Percentage:** The percentage of all queries with rating less than 3.

Find each `query_name`, the `quality`, and `poor_query_percentage`.
Both should be rounded to 2 decimal places.

---

## Real-Life Analogy

Imagine you are a search engine analyst. You want to evaluate the quality of different search queries.
- If a highly-rated result is at position 1, that's excellent (5/1 = 5).
- If a poorly-rated result is at position 200, that's terrible (1/200 = 0.005).
- You also want to know what percentage of results for a query are "poor" (rating < 3).

---

## Example Walkthrough

### Input: Queries table
| query_name | result           | position | rating |
|------------|------------------|----------|--------|
| Dog        | Golden Retriever | 1        | 5      |
| Dog        | German Shepherd  | 2        | 5      |
| Dog        | Mule             | 200      | 1      |
| Cat        | Shirazi          | 5        | 2      |
| Cat        | Siamese          | 3        | 3      |
| Cat        | Sphynx           | 7        | 4      |

### Step 1: Quality for Dog
- (5/1) + (5/2) + (1/200) = 5 + 2.5 + 0.005 = 7.505
- Average = 7.505 / 3 = **2.50**

### Step 2: Poor % for Dog
- Total = 3 queries.
- Poor (rating < 3) = 1 (Mule).
- (1 / 3) * 100 = **33.33**

### Output
| query_name | quality | poor_query_percentage |
|------------|---------|-----------------------|
| Dog        | 2.50    | 33.33                 |
| Cat        | 0.66    | 33.33                 |

---

## Final Query

```sql
SELECT 
    query_name,
    ROUND(AVG(rating / position), 2) AS quality,
    ROUND(SUM(CASE WHEN rating < 3 THEN 1 ELSE 0 END) / COUNT(*) * 100, 2) AS poor_query_percentage
FROM Queries
GROUP BY query_name;