# 1141. User Activity for the Past 30 Days I

**Difficulty:** Easy
**Topic:** Sorting and Grouping / Date Filtering
**LeetCode:** https://leetcode.com/problems/user-activity-for-the-past-30-days-i/
**Solved on:** 14/11/2026
**Runtime:** 475 ms (Beats 96.48%)
**Status:** Accepted (17/17 testcases passed)

---


## Problem Statement

**Table:** `Activity`

| Column Name   | Type |
|---------------|------|
| user_id       | int  |
| session_id    | int  |
| activity_date | date |
| activity_type | enum |

- This table may have duplicate rows.
- `activity_type` is an ENUM of type `('open_session', 'end_session', 'scroll_down', 'send_message')`.

### Task
Write a solution to find the **daily active user count** for a period of **30 days ending 2019-07-27 inclusively**.
A user was active on a day if they made at least one activity on that day.

Return the result table in any order.

**Note:** Any activity from `('open_session', 'end_session', 'scroll_down', 'send_message')` counts as valid.

---

## Real-Life Analogy

Imagine you run a social media app (like Facebook).
You have a log of user activities. You want to know how many unique users were active on each day in the last 30 days (from June 28 to July 27, 2019).

If a user performed multiple actions on the same day, they should only be counted **once** for that day.

---

## Example Walkthrough

### Input: Activity table
| user_id | session_id | activity_date | activity_type |
|---------|------------|---------------|---------------|
| 1       | 1          | 2019-07-20    | open_session  |
| 1       | 1          | 2019-07-20    | scroll_down   |
| 1       | 1          | 2019-07-20    | end_session   |
| 2       | 4          | 2019-07-20    | open_session  |
| 2       | 4          | 2019-07-21    | send_message  |
| 2       | 4          | 2019-07-21    | end_session   |
| 3       | 2          | 2019-07-21    | open_session  |
| 3       | 2          | 2019-07-21    | send_message  |
| 3       | 2          | 2019-07-21    | end_session   |
| 4       | 3          | 2019-06-25    | open_session  |
| 4       | 3          | 2019-06-25    | end_session   |

### Step 1: Filter the last 30 days (2019-06-28 to 2019-07-27)
- 2019-06-25 (User 4) is outside the range → excluded.

### Step 2: Count unique users per day
- 2019-07-20: User 1, User 2 → **2**
- 2019-07-21: User 2, User 3 → **2**

### Output
| day        | active_users |
|------------|--------------|
| 2019-07-20 | 2            |
| 2019-07-21 | 2            |

---

## Final Query (Approach 1: Using BETWEEN)

```sql
SELECT 
    activity_date AS day,
    COUNT(DISTINCT user_id) AS active_users
FROM Activity
WHERE activity_date BETWEEN '2019-06-28' AND '2019-07-27'
GROUP BY activity_date;