# 1148. Article Views I

**Difficulty:** Easy
**Topic:** Select / DISTINCT / ORDER BY
**LeetCode:** https://leetcode.com/problems/article-views-i/
**Solved on:** 9/10/2026
**Runtime:** 429 ms (Beats 70.73%)
**Status:** Accepted (13/13 testcases passed)

---


## Problem Statement

**Table:** `Views`

| Column Name | Type    |
|-------------|---------|
| article_id  | int     |
| author_id   | int     |
| viewer_id   | int     |
| view_date   | date    |

**Important Notes:**
- This table has **no primary key** — duplicate rows may exist
- Each row indicates that some viewer viewed an article (written by some author) on some date
- If `author_id = viewer_id`, it means the same person viewed their own article

### Task
Find all authors that viewed **at least one of their own articles**.

Return result **sorted by id in ascending order**.

---

## Understanding the Problem

I need to find the **ids of authors** who **viewed their own articles**.

Condition: `author_id = viewer_id`

But there is a problem:
- One author may view their own article multiple times
- If I just use the condition, **duplicate ids** will appear

So I use **`DISTINCT`** to remove duplicates.

The output column name should be **`id`** (not `author_id`) — so I use **`AS id`**.

The problem asks for **sorted** output — so I use **`ORDER BY id`**.

---

## Example Walkthrough

### Input Table (Views)

| article_id | author_id | viewer_id | view_date  |
|------------|-----------|-----------|------------|
| 1          | 3         | 5         | 2019-08-01 |
| 1          | 3         | 6         | 2019-08-02 |
| 2          | 7         | 7         | 2019-08-01 |
| 2          | 7         | 6         | 2019-08-02 |
| 4          | 7         | 1         | 2019-07-22 |
| 3          | 4         | 4         | 2019-07-21 |
| 3          | 4         | 4         | 2019-07-21 |

### Step 1: Check author_id = viewer_id

| article_id | author_id | viewer_id | Match? |
|------------|-----------|-----------|--------|
| 1          | 3         | 5         | NO     |
| 1          | 3         | 6         | NO     |
| 2          | 7         | 7         | YES    |
| 2          | 7         | 6         | NO     |
| 4          | 7         | 1         | NO     |
| 3          | 4         | 4         | YES    |
| 3          | 4         | 4         | YES    |

### Step 2: Remove duplicates

Matching author_id: 7, 4, 4

After DISTINCT: 7, 4

### Step 3: Sort ascending

4, 7

### Output

| id |
|----|
| 4  |
| 7  |

---

## Final Query

```sql
SELECT DISTINCT author_id AS id
FROM Views
WHERE author_id = viewer_id
ORDER BY id;