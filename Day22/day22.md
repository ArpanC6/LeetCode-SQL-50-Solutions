# 550. Game Play Analysis IV

**Difficulty:** Medium
**Topic:** Basic Aggregate Functions / CTE / JOIN
**LeetCode:** https://leetcode.com/problems/game-play-analysis-iv/
**Solved on:** 11/11/2026
**Runtime:** 450 ms (Beats 100.00%)
**Status:** Accepted (15/15 testcases passed)

---


## Problem Statement

**Table:** `Activity`

| Column Name  | Type |
|--------------|------|
| player_id    | int  |
| device_id    | int  |
| event_date   | date |
| games_played | int  |

- `(player_id, event_date)` is the primary key.
- Each row indicates a player logged in and played games on a specific date.

### Task
Find the **fraction of players** that logged in again on the day **after** the day they first logged in, rounded to 2 decimal places.

In other words: Find the number of players who logged in on the day immediately following their initial login, divided by the total number of players.

---

## Real-Life Analogy

Imagine you are a game developer. You want to know how many players come back the very next day after their first login.

- Player 1: First login 2016-03-01. Next login 2016-03-02 (YES, came back).
- Player 2: First login 2017-06-25. No login on 2017-06-26 (NO).
- Player 3: First login 2016-03-02. Next login 2018-07-03 (NO).

Total = 3 players. Came back next day = 1. Fraction = 1/3 = 0.33.

---

## Example Walkthrough

### Input: Activity table
| player_id | device_id | event_date | games_played |
|-----------|-----------|------------|--------------|
| 1         | 2         | 2016-03-01 | 5            |
| 1         | 2         | 2016-03-02 | 6            |
| 2         | 3         | 2017-06-25 | 1            |
| 3         | 1         | 2016-03-02 | 0            |
| 3         | 4         | 2018-07-03 | 5            |

### Step 1: Find each player's first login date
- Player 1: 2016-03-01
- Player 2: 2017-06-25
- Player 3: 2016-03-02

### Step 2: Check if they logged in on first_date + 1 day
- Player 1: Logged in on 2016-03-02 → YES
- Player 2: No login on 2017-06-26 → NO
- Player 3: No login on 2016-03-03 → NO

### Step 3: Compute fraction
- 1 out of 3 = 1/3 = 0.33

### Output
| fraction |
|----------|
| 0.33     |

---

## Final Query (Approach 1: Using CTE + JOIN — Best for Performance)

```sql
WITH FirstLogin AS (
    SELECT player_id, MIN(event_date) AS first_date
    FROM Activity
    GROUP BY player_id
)
SELECT 
    ROUND(
        COUNT(a.player_id) / (SELECT COUNT(DISTINCT player_id) FROM Activity), 
    2) AS fraction
FROM Activity a
JOIN FirstLogin f 
    ON a.player_id = f.player_id
    AND a.event_date = DATE_ADD(f.first_date, INTERVAL 1 DAY);