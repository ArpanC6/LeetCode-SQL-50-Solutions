# 2356. Number of Unique Subjects Taught by Each Teacher

**Difficulty:** Easy
**Topic:** Sorting and Grouping / Aggregation
**LeetCode:** https://leetcode.com/problems/number-of-unique-subjects-taught-by-each-teacher/
**Solved on:** 13/11/2026
**Runtime:** 485 ms (Beats 94.88%)
**Status:** Accepted (14/14 testcases passed)

---


## Problem Statement

**Table:** `Teacher`

| Column Name | Type |
|-------------|------|
| teacher_id  | int  |
| subject_id  | int  |
| dept_id     | int  |

- `(subject_id, dept_id)` is the primary key.
- Each row indicates that the teacher with `teacher_id` teaches the subject `subject_id` in the department `dept_id`.

### Task
Calculate the number of **unique subjects** each teacher teaches in the university.

Return the result table in any order.

---

## Real-Life Analogy

Imagine you are a university principal. You have a list of which teacher teaches which subject in which department.

A teacher might teach the same subject in **multiple departments**. But for the total count of subjects they teach, you only count that subject **once**.

For example:
- Teacher 1 teaches Subject 2 in dept 3 and dept 4 → counts as **1** unique subject (Subject 2).
- Teacher 1 teaches Subject 3 in dept 3 → counts as **1** unique subject (Subject 3).
- Total unique subjects for Teacher 1 = **2**.

---

## Example Walkthrough

### Input: Teacher table
| teacher_id | subject_id | dept_id |
|------------|------------|---------|
| 1          | 2          | 3       |
| 1          | 2          | 4       |
| 1          | 3          | 3       |
| 2          | 1          | 1       |
| 2          | 2          | 1       |
| 2          | 3          | 1       |
| 2          | 4          | 1       |

### Step 1: Group by teacher_id
- Teacher 1: 3 rows.
- Teacher 2: 4 rows.

### Step 2: Count unique subject_id per teacher
- Teacher 1: subjects {2, 3} → 2 unique.
- Teacher 2: subjects {1, 2, 3, 4} → 4 unique.

### Output
| teacher_id | cnt |
|------------|-----|
| 1          | 2   |
| 2          | 4   |

---

## Final Query

```sql
SELECT 
    teacher_id,
    COUNT(DISTINCT subject_id) AS cnt
FROM Teacher
GROUP BY teacher_id;