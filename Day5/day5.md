# 1683. Invalid Tweets

**Difficulty:** Easy
**Topic:** Select / String Functions
**LeetCode:** https://leetcode.com/problems/invalid-tweets/
**Solved on:** 9/10/2026
**Runtime:** 623 ms (Beats 64.52%)
**Status:** Accepted (22/22 testcases passed)

---

## Problem Statement

**Table:** `Tweets`

| Column Name | Type    |
|-------------|---------|
| tweet_id    | int     |
| content     | varchar |

- `tweet_id` is the primary key.
- `content` consists of alphanumeric characters, `!`, or ` ` (space) and no other special characters.
- This table contains all the tweets in a social media app.

### Task
Find the IDs of **invalid tweets**. A tweet is invalid if the **number of characters** used in the content is **strictly greater than 15**.

Return result in any order.

---

## Understanding the Problem

I need to find the **tweet_ids** where the **content is longer than 15 characters**.

The key idea:
1. Count the number of characters in `content`
2. Compare with 15
3. Return only those rows where length > 15

To count characters in MySQL, use `CHAR_LENGTH(content)`.

To check "strictly greater than 15", use `> 15` (not `>=`).

---

## Example Walkthrough

### Input Table (Tweets)

| tweet_id | content                           |
|----------|-----------------------------------|
| 1        | Let us Code                       |
| 2        | More than fifteen chars are here! |

### Step 1: Count characters

| tweet_id | content                           | CHAR_LENGTH |
|----------|-----------------------------------|-------------|
| 1        | Let us Code                       | 11          |
| 2        | More than fifteen chars are here! | 33          |

### Step 2: Check > 15

| tweet_id | CHAR_LENGTH | > 15? |
|----------|-------------|-------|
| 1        | 11          | NO    |
| 2        | 33          | YES   |

### Output

| tweet_id |
|----------|
| 2        |

**Explanation:**
- Tweet 1 has length = 11. It is a valid tweet.
- Tweet 2 has length = 33. It is an invalid tweet.

---

## Final Query

```sql
SELECT tweet_id
FROM Tweets
WHERE CHAR_LENGTH(content) > 15;