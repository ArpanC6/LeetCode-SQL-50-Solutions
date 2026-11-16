# 596. Classes With at Least 5 Students

**Difficulty:** Easy
**Topic:** Sorting and Grouping / HAVING
**LeetCode:** https://leetcode.com/problems/classes-with-at-least-5-students/
**Solved on:** 17/11/2026
**Runtime:** 591 ms (Beats 6.28%)
**Status:** Accepted (11/11 testcases passed)

---

## Problem Statement

**Table:** `Courses`

| Column Name | Type    |
|-------------|---------|
| student     | varchar |
| class       | varchar |

- `(student, class)` is the primary key.
- Each row indicates the name of a student and the class they are enrolled in.

### Task
Find all the classes that have **at least five students**.

Return the result table in any order.

---

## Real-Life Analogy

Imagine you are a school principal. You want to find out which classes have enough students (at least 5) to run. 
- You group the students by class.
- Count how many students are in each class.
- Only keep the classes where the count is 5 or more.

---

## Example Walkthrough

### Input: Courses table
| student | class    |
|---------|----------|
| A       | Math     |
| B       | English  |
| C       | Math     |
| D       | Biology  |
| E       | Math     |
| F       | Computer |
| G       | Math     |
| H       | Math     |
| I       | Math     |

### Step 1: Group by class and count students
- Math: 6 students
- English: 1 student
- Biology: 1 student
- Computer: 1 student

### Step 2: Filter with `HAVING COUNT(student) >= 5`
- Math is the only class with 5 or more students.

### Output
| class |
|-------|
| Math  |

---

## Final Query

```sql
SELECT class
FROM Courses
GROUP BY class
HAVING COUNT(student) >= 5;