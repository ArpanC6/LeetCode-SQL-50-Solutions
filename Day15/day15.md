# 620. Not Boring Movies

**Difficulty:** Easy
**Topic:** Basic Filtering / Modulo Operator
**LeetCode:** https://leetcode.com/problems/not-boring-movies/
**Solved on:** 26/10/2026
**Runtime:** 462 ms (Beats 5.93%)
**Status:** Accepted (11/11 testcases passed)

---


## Problem Statement

**Table:** `Cinema`

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| movie       | varchar |
| description | varchar |
| rating      | float   |

- `id` is the primary key.
- Each row contains info about a movie, its genre, and its rating.
- `rating` is a 2 decimal places float in the range [0, 10].

### Task
Report the movies with an **odd-numbered ID** and a **description that is not "boring"**.

Return the result table ordered by `rating` in **descending order**.

---

## Real-Life Analogy

Imagine you manage a cinema. You want to show a list of movies that:
1. Have an odd ID (e.g., 1, 3, 5).
2. Are NOT boring.
3. Are sorted from highest rating to lowest.

This is a simple filtering problem. We use the **modulo operator (`%`)** to check for odd numbers and `<>` (or `!=`) to filter out the word "boring".

---

## Example Walkthrough

### Input: Cinema table
| id | movie      | description | rating |
|----|------------|-------------|--------|
| 1  | War        | great 3D    | 8.9    |
| 2  | Science    | fiction     | 8.5    |
| 3  | irish      | boring      | 6.2    |
| 4  | Ice song   | Fantacy     | 8.6    |
| 5  | House card | Interesting | 9.1    |

### Step 1: Filter Odd IDs
- ID 1 (Odd), ID 3 (Odd), ID 5 (Odd).

### Step 2: Filter NOT 'boring'
- ID 1: "great 3D" (Keep)
- ID 3: "boring" (Remove)
- ID 5: "Interesting" (Keep)

### Step 3: Sort by Rating (DESC)
- ID 5 (Rating: 9.1)
- ID 1 (Rating: 8.9)

### Output
| id | movie      | description | rating |
|----|------------|-------------|--------|
| 5  | House card | Interesting | 9.1    |
| 1  | War        | great 3D    | 8.9    |

---

## Final Query

```sql
SELECT id, movie, description, rating
FROM Cinema
WHERE id % 2 <> 0
  AND description <> 'boring'
ORDER BY rating DESC;