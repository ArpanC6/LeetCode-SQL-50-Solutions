# 1934. Confirmation Rate

**Difficulty:** Medium
**Topic:** Basic Joins / LEFT JOIN / Aggregate Functions
**LeetCode:** https://leetcode.com/problems/confirmation-rate/
**Solved on:** 25/10/2026
**Runtime:** 966 ms (Beats 11.63%)
**Status:** Accepted (14/14 testcases passed)

---

## Visual Guide (One-Page Summary)

![1934 Visual Guide](./1934_Confirmation_Rate.png)

---

## Problem Statement

**Table 1:** `Signups`

| Column Name | Type     |
|-------------|----------|
| user_id     | int      |
| time_stamp  | datetime |

- `user_id` is the primary key.
- Each row contains the signup time for the user with ID `user_id`.

**Table 2:** `Confirmations`

| Column Name | Type     |
|-------------|----------|
| user_id     | int      |
| time_stamp  | datetime |
| action      | ENUM     |

- `(user_id, time_stamp)` is the primary key.
- `user_id` is a foreign key to the `Signups` table.
- `action` is an ENUM of type `('confirmed', 'timeout')`.
- Each row indicates a user requested a confirmation message and it was either confirmed or timed out.

### Task
The confirmation rate of a user is the number of `'confirmed'` messages divided by the total number of requested confirmation messages. The confirmation rate of a user that did not request any confirmation messages is **0**.

Find the confirmation rate of each user.
Round the confirmation rate to **two decimal places**.

Return result in any order.

---

## Real-Life Analogy

Imagine you run an app. When users sign up, you send them a verification message.
- If they click it -> `confirmed`
- If time runs out -> `timeout`

You want to calculate the **verification success rate** for each user. 
If a user never triggered a verification message (like User 6), their rate is `0.00`.

---

## Example Walkthrough

### Input: Signups
| user_id | time_stamp          |
|---------|---------------------|
| 3       | 2020-03-21 10:16:13 |
| 7       | 2020-01-04 13:57:59 |
| 2       | 2020-07-29 23:09:44 |
| 6       | 2020-12-09 10:39:37 |

### Input: Confirmations
| user_id | time_stamp          | action    |
|---------|---------------------|-----------|
| 3       | 2021-01-06 03:30:46 | timeout   |
| 3       | 2021-07-14 14:00:00 | timeout   |
| 7       | 2021-06-12 11:57:29 | confirmed |
| 7       | 2021-06-13 12:58:28 | confirmed |
| 7       | 2021-06-14 13:59:27 | confirmed |
| 2       | 2021-01-22 00:00:00 | confirmed |
| 2       | 2021-02-28 23:59:59 | timeout   |

### Output
| user_id | confirmation_rate |
|---------|-------------------|
| 6       | 0.00              |
| 3       | 0.00              |
| 7       | 1.00              |
| 2       | 0.50              |

### Explanation
- User 6: no requests -> rate = 0.00
- User 3: 2 requests, 0 confirmed -> 0 / 2 = 0.00
- User 7: 3 requests, 3 confirmed -> 3 / 3 = 1.00
- User 2: 2 requests, 1 confirmed -> 1 / 2 = 0.50

---

## Final Query (Approach 1: Using AVG — Recommended)

```sql
SELECT 
    s.user_id,
    ROUND(IFNULL(AVG(c.action = 'confirmed'), 0), 2) AS confirmation_rate
FROM Signups s
LEFT JOIN Confirmations c 
    ON s.user_id = c.user_id
GROUP BY s.user_id;