# 1633. Percentage of Users Attended a Contest

**Difficulty:** Easy
**Topic:** Basic Aggregate Functions / Subqueries
**LeetCode:** https://leetcode.com/problems/percentage-of-users-attended-a-contest/
**Solved on:** 01/11/2026
**Runtime:** 1696 ms (Beats 5.77%)
**Status:** Accepted (14/14 testcases passed)

---


## Problem Statement

**Table 1:** `Users`

| Column Name | Type    |
|-------------|---------|
| user_id     | int     |
| user_name   | varchar |

- `user_id` is the primary key.
- Each row contains the name and id of a user.

**Table 2:** `Register`

| Column Name | Type |
|-------------|------|
| contest_id  | int  |
| user_id     | int  |

- `(contest_id, user_id)` is the primary key.
- Each row indicates a user registered for a contest.

### Task
Find the percentage of users registered in each contest, rounded to **two decimal places**.

Return the result table ordered by:
1. `percentage` in **descending order**.
2. In case of a tie, order by `contest_id` in **ascending order**.

---

## Real-Life Analogy

Imagine you are a cultural secretary of a college. 
- There are a total of **3 students** (Users table).
- A list of who registered for which contest (Register table).

You want to find the percentage of total students who registered for each contest.
- Formula: `(Number of users in that contest / Total users) * 100`

For example, if 2 out of 3 students registered for Contest 215, the percentage is `(2/3) * 100 = 66.67%`.

---

## Example Walkthrough

### Input: Users
| user_id | user_name |
|---------|-----------|
| 6       | Alice     |
| 2       | Bob       |
| 7       | Alex      |

### Input: Register
| contest_id | user_id |
|------------|---------|
| 215        | 6       |
| 209        | 2       |
| 208        | 2       |
| 210        | 6       |
| 208        | 6       |
| 209        | 7       |
| 209        | 6       |
| 215        | 7       |
| 208        | 7       |
| 210        | 2       |
| 207        | 2       |
| 210        | 7       |

### Step 1: Total Users
`SELECT COUNT(*) FROM Users` = **3**

### Step 2: Count per contest
- Contest 208: 3 users
- Contest 209: 3 users
- Contest 210: 3 users
- Contest 215: 2 users
- Contest 207: 1 user

### Step 3: Calculate Percentage
- Contest 208: (3 / 3) * 100 = **100.00%**
- Contest 215: (2 / 3) * 100 = **66.67%**
- Contest 207: (1 / 3) * 100 = **33.33%**

### Step 4: Sort
- First by percentage DESC, then by contest_id ASC.

### Output
| contest_id | percentage |
|------------|------------|
| 208        | 100.0      |
| 209        | 100.0      |
| 210        | 100.0      |
| 215        | 66.67      |
| 207        | 33.33      |

---

## Final Query

```sql
SELECT 
    r.contest_id,
    ROUND((COUNT(DISTINCT r.user_id) * 100.0) / (SELECT COUNT(*) FROM Users), 2) AS percentage
FROM Register r
GROUP BY r.contest_id
ORDER BY percentage DESC, r.contest_id ASC;