# 570. Managers with at Least 5 Direct Reports

**Difficulty:** Medium
**Topic:** Basic Joins / SELF JOIN / HAVING
**LeetCode:** https://leetcode.com/problems/managers-with-at-least-5-direct-reports/
**Solved on:** 23/10/2026
**Runtime:** 411 ms (Beats 27.41%)
**Status:** Accepted (11/11 testcases passed)

---


## Problem Statement

**Table:** `Employee`

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |
| department  | varchar |
| managerId   | int     |

- `id` is the primary key.
- Each row contains the employee's name, department, and the `id` of their manager.
- If `managerId` is null, the employee does not have a manager.
- No employee will be the manager of themself.

### Task
Find managers with **at least five direct reports**.

Return result in any order.

---

## Real-Life Analogy

Imagine you are an HR manager. You have one big employee register that shows every employee and their boss's ID.

Your boss asks you: "Give me the names of all managers who have **5 or more people reporting directly to them**."

You need to:
1. Match each manager's `id` with employees' `managerId`.
2. Count how many employees report to each manager.
3. Keep only those with 5 or more.

This requires a **SELF JOIN** because the data is in one table.

---

## Understanding the Problem

We have only **ONE table** (`Employee`).

- `id` = employee's ID
- `managerId` = the ID of their boss

To find who reports to whom:
- Employee's `managerId` → Manager's `id`

We use a **SELF JOIN** to bring both roles into one row:
- `e1` = Manager (boss)
- `e2` = Reportee (subordinate)

Then we group by manager and count reportees using `COUNT(e2.id)`, filtering with `HAVING COUNT(e2.id) >= 5`.

---

## Example Walkthrough

### Input: Employee table

| id  | name  | department | managerId |
|-----|-------|------------|-----------|
| 101 | John  | A          | null      |
| 102 | Dan   | A          | 101       |
| 103 | James | A          | 101       |
| 104 | Amy   | A          | 101       |
| 105 | Anne  | A          | 101       |
| 106 | Ron   | B          | 101       |

### Step 1: SELF JOIN (match manager to reportees)

`e1` = Manager, `e2` = Reportee

| e1.id (Manager) | e1.name | e2.id (Reportee) | e2.name |
|-----------------|---------|------------------|---------|
| 101             | John    | 102              | Dan     |
| 101             | John    | 103              | James   |
| 101             | John    | 104              | Amy     |
| 101             | John    | 105              | Anne    |
| 101             | John    | 106              | Ron     |

### Step 2: Count reportees per manager

| Manager | Count |
|---------|-------|
| John    | 5     |

### Step 3: Filter by COUNT >= 5

John has exactly 5 → include.

### Output

| name |
|------|
| John |

---

## Final Query

```sql
SELECT e1.name
FROM Employee e1
JOIN Employee e2 
    ON e1.id = e2.managerId
GROUP BY e1.id, e1.name
HAVING COUNT(e2.id) >= 5;