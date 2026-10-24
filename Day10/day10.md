# 1661. Average Time of Process per Machine

**Difficulty:** Easy
**Topic:** Basic Joins / SELF JOIN + AGGREGATE
**LeetCode:** https://leetcode.com/problems/average-time-of-process-per-machine/
**Solved on:** 16/10/2026
**Runtime:** [X] ms (Beats [X]%)
**Status:** Accepted ([X]/[X] testcases passed)

---


## Problem Statement

**Table:** `Activity`

| Column Name    | Type    |
|----------------|---------|
| machine_id     | int     |
| process_id     | int     |
| activity_type  | enum    |
| timestamp      | float   |

- `(machine_id, process_id, activity_type)` is the primary key.
- `machine_id` is the ID of a machine.
- `process_id` is the ID of a process running on that machine.
- `activity_type` is an ENUM of type `('start', 'end')`.
- `timestamp` is a float representing current time in seconds.
- `'start'` means the machine starts the process, `'end'` means it ends.
- `start` timestamp is always ≤ `end` timestamp for every `(machine_id, process_id)` pair.
- Every `(machine_id, process_id)` pair has both a `'start'` and an `'end'`.

### Task
Find the **average time** each machine takes to complete a process.

- Processing time = `end` timestamp - `start` timestamp
- Average time = total time to complete all processes ÷ number of processes on that machine
- Result columns: `machine_id`, `processing_time`
- Round `processing_time` to **3 decimal places**
- Return result in any order

---

## Real-Life Analogy

Imagine you are the manager of a factory. Each machine runs several processes. For each process, you have a "start" record and an "end" record (two separate rows).

You want to know: **On average, how long does each machine take to complete one process?**

To find this:
1. For each process, calculate `end - start`
2. For each machine, take the average of all its processes' times

The key challenge: `start` and `end` are in **two separate rows**. We must join them back together — a **SELF JOIN**.

---

## Understanding the Problem

We have only **ONE table**. Each `(machine_id, process_id)` pair has:
- One row with `activity_type = 'start'`
- One row with `activity_type = 'end'`

To compute `end - start`, we must join these two rows together.

Key insight: Join the table with itself, matching:
1. Same `machine_id`
2. Same `process_id`
3. `a` row is `'start'`, `b` row is `'end'`

Then: `AVG(b.timestamp - a.timestamp)` grouped by `machine_id`.

---

## What is SELF JOIN?

**SELF JOIN** means using the **same table twice** with **two different aliases**.

```sql
FROM Activity a
INNER JOIN Activity b ON ...