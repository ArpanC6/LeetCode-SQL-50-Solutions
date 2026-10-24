# 577. Employee Bonus

**Difficulty:** Easy
**Topic:** Basic Joins / LEFT JOIN / NULL Handling
**LeetCode:** https://leetcode.com/problems/employee-bonus/
**Solved on:** 17/10/2026
**Runtime:** 1085 ms (Beats 48.09%)
**Status:** Accepted (21/21 testcases passed)

---

## Problem Statement

**Table 1:** `Employee`

| Column Name | Type    |
|-------------|---------|
| empId       | int     |
| name        | varchar |
| supervisor  | int     |
| salary      | int     |

- `empId` is the primary key.
- Each row indicates the name, ID, salary, and manager's ID of an employee.

**Table 2:** `Bonus`

| Column Name | Type |
|-------------|------|
| empId       | int  |
| bonus       | int  |

- `empId` is unique.
- `empId` is a foreign key referencing `Employee.empId`.
- Each row contains the ID of an employee and their bonus.

### Task
Report the `name` and `bonus` amount of each employee who satisfies **either** of the following:
1. The employee has a bonus **less than 1000**.
2. The employee **did not get any bonus**.

Return result in any order.

---

## Real-Life Analogy

Imagine you are an HR manager. You have two lists:
- **Employee list** — all employees
- **Bonus list** — only those who received a bonus

You want to find employees who either:
- Got a very small bonus (less than 1000)
- Got no bonus at all

Employees who got a big bonus (1000 or more) are excluded.

This is a classic **LEFT JOIN** problem because:
- We want **all employees** (even those without a bonus)
- Some employees have no matching record in the Bonus table

---

## Understanding the Problem

We have 2 tables:
1. `Employee` — all employees (4 rows)
2. `Bonus` — only employees with a bonus (2 rows)

We need to:
1. Keep all employees (using LEFT JOIN)
2. Show their bonus if they have one, or NULL if they don't
3. Filter for: `bonus < 1000` OR `bonus IS NULL`

**Key challenge:** NULL handling. `NULL < 1000` is not TRUE — it's NULL (unknown), so those rows get filtered out if we don't use `IS NULL` explicitly.

---

## Example Walkthrough

### Input: Employee table

| empId | name   | supervisor | salary |
|-------|--------|------------|--------|
| 3     | Brad   | null       | 4000   |
| 1     | John   | 3          | 1000   |
| 2     | Dan    | 3          | 2000   |
| 4     | Thomas | 3          | 4000   |

### Input: Bonus table

| empId | bonus |
|-------|-------|
| 2     | 500   |
| 4     | 2000  |

### Step 1: Check each employee's bonus

| empId | name   | Bonus table has entry? | bonus |
|-------|--------|------------------------|-------|
| 3     | Brad   | NO                     | NULL  |
| 1     | John   | NO                     | NULL  |
| 2     | Dan    | YES                    | 500   |
| 4     | Thomas | YES                    | 2000  |

### Step 2: Apply filter (bonus < 1000 OR bonus IS NULL)

| empId | name   | bonus | < 1000? | IS NULL? | Include? |
|-------|--------|-------|---------|----------|----------|
| 3     | Brad   | NULL  | NO (NULL) | YES    | YES      |
| 1     | John   | NULL  | NO (NULL) | YES    | YES      |
| 2     | Dan    | 500   | YES     | NO       | YES      |
| 4     | Thomas | 2000  | NO      | NO       | NO       |

### Output

| name | bonus |
|------|-------|
| Brad | null  |
| John | null  |
| Dan  | 500   |

---

## Final Query

```sql
SELECT name, bonus
FROM Employee e
LEFT JOIN Bonus b ON e.empId = b.empId
WHERE b.bonus < 1000 OR b.bonus IS NULL;