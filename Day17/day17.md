# 1075. Project Employees I

**Difficulty:** Easy
**Topic:** Basic Joins / Aggregate Functions
**LeetCode:** https://leetcode.com/problems/project-employees-i/
**Solved on:** 31/10/2026
**Runtime:** 601 ms (Beats 37.07%)
**Status:** Accepted (8/8 testcases passed)

---


## Problem Statement

**Table 1:** `Project`

| Column Name | Type |
|-------------|------|
| project_id  | int  |
| employee_id | int  |

- `(project_id, employee_id)` is the primary key.
- `employee_id` is a foreign key to the `Employee` table.
- Each row indicates that the employee is working on the project.

**Table 2:** `Employee`

| Column Name      | Type    |
|------------------|---------|
| employee_id      | int     |
| name             | varchar |
| experience_years | int     |

- `employee_id` is the primary key.
- `experience_years` is guaranteed to be NOT NULL.

### Task
Write a query that reports the **average experience years** of all employees for each project, rounded to **2 digits**.

Return result in any order.

---

## Real-Life Analogy

Imagine you are an HR manager. You have two registers:
1. **Project Register:** Who is working on which project.
2. **Employee Register:** How many years of experience each employee has.

You want to calculate the average experience of employees working on each project.

- Project 1: Employees 1, 2, 3 -> Experiences: 3, 2, 1 -> Average = (3+2+1)/3 = 2.00
- Project 2: Employees 1, 4 -> Experiences: 3, 2 -> Average = (3+2)/2 = 2.50

---

## Example Walkthrough

### Input: Project
| project_id | employee_id |
|------------|-------------|
| 1          | 1           |
| 1          | 2           |
| 1          | 3           |
| 2          | 1           |
| 2          | 4           |

### Input: Employee
| employee_id | name   | experience_years |
|-------------|--------|------------------|
| 1           | Khaled | 3                |
| 2           | Ali    | 2                |
| 3           | John   | 1                |
| 4           | Doe    | 2                |

### Step 1: Join both tables on `employee_id`

| project_id | employee_id | name   | experience_years |
|------------|-------------|--------|------------------|
| 1          | 1           | Khaled | 3                |
| 1          | 2           | Ali    | 2                |
| 1          | 3           | John   | 1                |
| 2          | 1           | Khaled | 3                |
| 2          | 4           | Doe    | 2                |

### Step 2: Group by `project_id` and compute AVG

| project_id | average_years |
|------------|---------------|
| 1          | (3+2+1)/3 = 2.00 |
| 2          | (3+2)/2 = 2.50 |

### Output
| project_id | average_years |
|------------|---------------|
| 1          | 2.00          |
| 2          | 2.50          |

---

## Final Query

```sql
SELECT 
    p.project_id,
    ROUND(AVG(e.experience_years), 2) AS average_years
FROM Project p
LEFT JOIN Employee e 
    ON p.employee_id = e.employee_id
GROUP BY p.project_id;