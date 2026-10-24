# 1280. Students and Examinations

**Difficulty:** Easy
**Topic:** Basic Joins / CROSS JOIN / LEFT JOIN
**LeetCode:** https://leetcode.com/problems/students-and-examinations/
**Solved on:** 23/10/2026
**Status:** Accepted (10/10 testcases passed)

---

## Problem Statement

**Table 1:** `Students`

| Column Name | Type    |
|-------------|---------|
| student_id  | int     |
| student_name| varchar |

- `student_id` is the primary key.

**Table 2:** `Subjects`

| Column Name | Type    |
|-------------|---------|
| subject_name| varchar |

- `subject_name` is the primary key.

**Table 3:** `Examinations`

| Column Name | Type    |
|-------------|---------|
| student_id  | int     |
| subject_name| varchar |

- No primary key, may contain duplicates.
- Each row indicates a student attended an exam of a subject.

### Task
Find the number of times each student attended each exam.

Return result ordered by `student_id` and `subject_name`.

---

## Real-Life Analogy

Imagine you are a school principal. You have:
- A list of all **students**.
- A list of all **subjects**.
- A list of **exam attendance** (who took what, and how many times).

Every student must take every subject. So you need to create a "Master List" (Student × Subject) and count how many times they attended each exam. Even if a student didn't attend a subject (like Alex), they must appear with a count of **0**.

---

## Understanding the Problem

We have 3 tables. To get all combinations of students and subjects, we need a **CROSS JOIN**. Then, we attach the `Examinations` table using a **LEFT JOIN** to preserve all combinations.

**Key Challenge:** Using `COUNT(c.student_id)` instead of `COUNT(*)` so that missing exams result in `0`, not `1`.

---

## Example Walkthrough

### Input: Students
| student_id | student_name |
|------------|--------------|
| 1          | Alice        |
| 2          | Bob          |
| 13         | John         |
| 6          | Alex         |

### Input: Subjects
| subject_name |
|--------------|
| Math         |
| Physics      |
| Programming  |

### Input: Examinations (partial)
| student_id | subject_name |
|------------|--------------|
| 1          | Math         |
| 1          | Math         | *(Alice took Math twice)*
| 1          | Physics      |
...

### Step 1: CROSS JOIN (Master List)
Create 4 × 3 = 12 rows of all student-subject combinations.

### Step 2: LEFT JOIN + COUNT
Attach exams. For Alice & Math, there are 3 matching rows, so `COUNT` = 3.
For Alex & Math, there are no matching rows (`NULL`), so `COUNT` = 0.

### Output
| student_id | student_name | subject_name | attended_exams |
|------------|--------------|--------------|----------------|
| 1          | Alice        | Math         | 3              |
| 1          | Alice        | Physics      | 2              |
| 1          | Alice        | Programming  | 1              |
| 2          | Bob          | Math         | 1              |
| 2          | Bob          | Physics      | 0              |
| 2          | Bob          | Programming  | 1              |
| 6          | Alex         | Math         | 0              |
| 6          | Alex         | Physics      | 0              |
| 6          | Alex         | Programming  | 0              |
| 13         | John         | Math         | 1              |
| 13         | John         | Physics      | 1              |
| 13         | John         | Programming  | 1              |

---

## Final Query

```sql
SELECT 
    a.student_id, 
    a.student_name, 
    b.subject_name, 
    COUNT(c.student_id) AS attended_exams
FROM Students a
CROSS JOIN Subjects b
LEFT JOIN Examinations c 
    ON a.student_id = c.student_id 
    AND b.subject_name = c.subject_name
GROUP BY a.student_id, a.student_name, b.subject_name
ORDER BY a.student_id, b.subject_name;