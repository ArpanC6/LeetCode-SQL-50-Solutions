# 1378. Replace Employee ID With The Unique Identifier

**Difficulty:** Easy
**Topic:** Basic Joins / LEFT JOIN
**LeetCode:** https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/
**Solved on:** 10/10/2026
**Runtime:** 1263 ms (Beats 64.33%)
**Status:** Accepted (25/25 testcases passed)

---


## Problem Statement

**Table 1:** `Employees`

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |

- `id` is the primary key.
- Each row contains the id and name of an employee.

**Table 2:** `EmployeeUNI`

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| unique_id   | int     |

- `(id, unique_id)` is the primary key.
- Each row contains the id and corresponding unique id of an employee.

### Task
Show the **unique_id** of each user. If a user does not have a unique_id, show **null** instead.

Return result in any order.

---

## Real-Life Analogy

Imagine you are the principal of a school. You have 2 registers:

**Register 1 — Students Register (Employees table):**
- Contains all students in the school
- 5 students: Alice, Bob, Meir, Winston, Jonathan

**Register 2 — Library Card Register (EmployeeUNI table):**
- Contains info about students who got library cards
- Only 3 students: Meir, Winston, Jonathan

**What do you want to do?**
- Create a list where **all students** are present
- Students who have library cards: show their card number
- Students who don't: show blank (NULL)

This task in SQL is called **LEFT JOIN**.

---

## Understanding the Problem

We have 2 tables:
1. `Employees` — all employees (5 people)
2. `EmployeeUNI` — unique_id only for 3 people

What we need to do:
1. Keep **all employees** from the Employees table
2. Bring in `unique_id` from EmployeeUNI table
3. If a match exists, show `unique_id`
4. If no match, show **NULL**

This is a classic **LEFT JOIN** example.

---

## Why LEFT JOIN (not INNER JOIN)?

| JOIN Type | What It Does | Result |
|-----------|--------------|--------|
| **INNER JOIN** | Only matching rows | Alice and Bob missing |
| **LEFT JOIN** | All rows from left + matching from right | Alice and Bob shown with NULL |

The problem says: **"If a user does not have a unique ID, show null"** — meaning Alice and Bob must also appear.

So we use **LEFT JOIN**.

---

## Example Walkthrough

### Input: Employees table

| id | name     |
|----|----------|
| 1  | Alice    |
| 7  | Bob      |
| 11 | Meir     |
| 90 | Winston  |
| 3  | Jonathan |

### Input: EmployeeUNI table

| id | unique_id |
|----|-----------|
| 3  | 1         |
| 11 | 2         |
| 90 | 3         |

### Step 1: Check each employee

| Employee id | name     | Match in EmployeeUNI? | unique_id |
|-------------|----------|----------------------|-----------|
| 1           | Alice    | NO                   | NULL      |
| 7           | Bob      | NO                   | NULL      |
| 11          | Meir     | YES (unique_id=2)    | 2         |
| 90          | Winston  | YES (unique_id=3)    | 3         |
| 3           | Jonathan | YES (unique_id=1)    | 1         |

### Output

| unique_id | name     |
|-----------|----------|
| null      | Alice    |
| null      | Bob      |
| 2         | Meir     |
| 3         | Winston  |
| 1         | Jonathan |

---

## Final Query

```sql
SELECT unique_id, name
FROM Employees
LEFT JOIN EmployeeUNI 
    ON Employees.id = EmployeeUNI.id;