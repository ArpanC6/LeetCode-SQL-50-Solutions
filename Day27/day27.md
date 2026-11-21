# 1729. Find Followers Count

**Difficulty:** Easy
**Topic:** Sorting and Grouping / Aggregation
**LeetCode:** https://leetcode.com/problems/find-followers-count/
**Solved on:** 21/11/2026
**Runtime:** 680 ms (Beats 40.45%) *(Note: Using DISTINCT)*
**Status:** Accepted (22/22 testcases passed)

---


## Problem Statement

**Table:** `Followers`

| Column Name | Type |
|-------------|------|
| user_id     | int  |
| follower_id | int  |

- `(user_id, follower_id)` is the primary key (combination of columns with unique values) for this table.
- This table contains the IDs of a user and a follower in a social media app where the follower follows the user.

### Task
Write a solution that will, for each user, return the **number of followers**.

Return the result table ordered by `user_id` in **ascending order**.

---

## Real-Life Analogy

Imagine you are a social media manager. You want to know how many followers each user has. 
- User 0 is followed by User 1 (1 follower).
- User 1 is followed by User 0 (1 follower).
- User 2 is followed by Users 0 and 1 (2 followers).

---

## Example Walkthrough

### Input: Followers table
| user_id | follower_id |
|---------|-------------|
| 0       | 1           |
| 1       | 0           |
| 2       | 0           |
| 2       | 1           |

### Output
| user_id | followers_count |
|---------|-----------------|
| 0       | 1               |
| 1       | 1               |
| 2       | 2               |

---

## Final Query (Approach 1: Simple COUNT - Recommended)

```sql
SELECT 
    user_id,
    COUNT(follower_id) AS followers_count
FROM Followers
GROUP BY user_id
ORDER BY user_id;