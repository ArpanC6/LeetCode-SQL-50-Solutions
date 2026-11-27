# Day 30: 1731. The Number of Employees Which Report to Each Employee

| Detail | Value |
|---|---|
| Difficulty | Easy |
| Section | Advanced Select and Joins |
| Language | MySQL |
| Status | Accepted |
| Testcases Passed | 24 / 24 |
| Runtime | 531 ms |
| Beats | 98.10% |
| Solved On | 27/11/2026 |

---

## Problem Statement

Table `Employees` has the columns `employee_id`, `name`, `reports_to` and `age`.

A **manager** is an employee with at least one other employee reporting directly to them. For every manager, return:

- `employee_id` and `name`
- `reports_count`: number of direct reports
- `average_age`: average age of those reports, rounded to the nearest integer

Order the result by `employee_id`.

## Example

**Input**

| employee_id | name | reports_to | age |
|---|---|---|---|
| 9 | Hercy | null | 43 |
| 6 | Alice | 9 | 41 |
| 4 | Bob | 9 | 36 |
| 2 | Winston | null | 37 |

**Output**

| employee_id | name | reports_count | average_age |
|---|---|---|---|
| 9 | Hercy | 2 | 39 |

---

## Analogy: The Office Slip

Every employee holds a slip with their boss's ID written on it (`reports_to`).

- Alice's slip says 9, so her boss is Hercy.
- Bob's slip says 9, so his boss is also Hercy.
- Hercy and Winston have blank slips (`null`).
- Winston's ID is on nobody's slip, so he is not a manager.

The slip only has an ID. The boss's name is in another row of the same table, so we join the table with itself.

---

## Step-by-Step Build

### Step 1: Use the table twice (Self Join)

- `e` = the employee who reports
- `m` = the manager who receives the report

### Step 2: Match the two copies

```sql
FROM Employees e
JOIN Employees m
  ON e.reports_to = m.employee_id
```

| e.name | e.age | e.reports_to | m.employee_id | m.name |
|---|---|---|---|---|
| Alice | 41 | 9 | 9 | Hercy |
| Bob | 36 | 9 | 9 | Hercy |

Rows with `reports_to = null` match nothing, so the inner join drops them from the `e` side.

### Step 3: Group by manager

```sql
GROUP BY m.employee_id, m.name
```

Each manager gets a separate group.

### Step 4: Calculate per group

| Calculation | Expression | Result for Hercy |
|---|---|---|
| Number of reports | `COUNT(e.employee_id)` | 2 |
| Average age | `AVG(e.age)` | 38.5 |
| Rounded | `ROUND(AVG(e.age))` | 39 |

---

## Final Query

```sql
SELECT m.employee_id,
       m.name,
       COUNT(e.employee_id) AS reports_count,
       ROUND(AVG(e.age)) AS average_age
FROM Employees e
JOIN Employees m
  ON e.reports_to = m.employee_id
GROUP BY m.employee_id, m.name
ORDER BY m.employee_id;
```

## Execution Order

1. `FROM` and `JOIN`: pair each employee with their manager
2. `GROUP BY`: make one group per manager
3. `SELECT`: calculate the count and rounded average
4. `ORDER BY`: sort by manager ID

---

## Key Concepts

- **Self Join:** joining a table with itself using two aliases
- **COUNT:** counts the reports in each group
- **AVG:** finds the average age in each group
- **ROUND:** rounds to the nearest integer
- **GROUP BY:** applies the aggregates to each manager separately

## Common Mistakes

- Reversing the join as `e.employee_id = m.reports_to` while keeping the same `SELECT`, which swaps the roles of the two copies
- Using `m.age` instead of `e.age` for the average
- Selecting `e.name` instead of `m.name`
- Forgetting `GROUP BY`, so all rows are treated as one group
- Forgetting `ORDER BY`, which the problem requires

## Interview Tips

- State the roles first: `e` is the employee, `m` is the manager.
- Explain that an inner join automatically excludes employees with no reports from the manager list.
- Explain why `LEFT JOIN` is not needed: only managers with at least one report are required.

## Key Takeaways

- When a column points to another row in the same table, think of a self join.
- Display details from the manager copy and aggregate data from the employee copy.