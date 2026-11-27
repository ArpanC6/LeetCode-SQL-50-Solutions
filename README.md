<h1 align="center">LeetCode SQL 50 - Solutions and Notes</h1>

<p align="center">
  A day-by-day record of solving the LeetCode SQL 50 study plan in MySQL,<br>
  with a clear explanation, a clean query and revision notes for every problem.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Language-MySQL-blue?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL">
  <img src="https://img.shields.io/badge/Platform-LeetCode-orange?style=for-the-badge&logo=leetcode&logoColor=white" alt="LeetCode">
  <img src="https://img.shields.io/badge/Progress-30%2F50-brightgreen?style=for-the-badge" alt="Progress 30/50">
  <img src="https://img.shields.io/badge/Status-In%20Progress-yellow?style=for-the-badge" alt="Status">
</p>

<p align="center">
  <a href="https://github.com/ArpanC6/LeetCode-SQL-50-Solutions/stargazers">
    <img src="https://img.shields.io/badge/Star%20this%20repository-if%20it%20helps%20you-brightgreen?style=for-the-badge" alt="Star this repository">
  </a>
</p>

---

## Table of Contents

1. [About](#about)
2. [Progress Overview](#progress-overview)
3. [Daily Solutions](#daily-solutions)
4. [Revise by Pattern](#revise-by-pattern)
5. [Full Problem List](#full-problem-list)
6. [What Each Notes File Contains](#what-each-notes-file-contains)
7. [Repository Structure](#repository-structure)
8. [Core SQL Concepts Covered](#core-sql-concepts-covered)
9. [How to Use This Repository](#how-to-use-this-repository)
10. [Author](#author)

---

## About

This repository tracks my progress through the **LeetCode SQL 50** study plan.
One problem is solved and documented every day. The goal is not only to get
an Accepted verdict, but to understand why the query works, so that the same
idea can be rebuilt from scratch in an interview.

Every problem includes:

- The problem statement and a worked example
- A real-life analogy to build intuition
- A step-by-step build-up of the query
- The final accepted query
- Common mistakes and interview tips

> This repository is updated daily.

---

## Progress Overview

**Overall: 30 of 50 problems solved (60%)**

| Category | Solved | Total | Progress | Status |
|:---|:---:|:---:|:---|:---:|
| 01. Select | 5 | 5 | `██████████` | Complete |
| 02. Basic Joins | 9 | 9 | `██████████` | Complete |
| 03. Basic Aggregate Functions | 8 | 8 | `██████████` | Complete |
| 04. Sorting and Grouping | 7 | 7 | `██████████` | Complete |
| 05. Advanced Select and Joins | 1 | 7 | `█░░░░░░░░░` | In progress |
| 06. Subqueries | 0 | 7 | `░░░░░░░░░░` | Not started |
| 07. Advanced String Functions / Regex / Clause | 0 | 7 | `░░░░░░░░░░` | Not started |

**By difficulty**

| Difficulty | Solved | Total |
|:---|:---:|:---:|
| Easy | 23 | 32 |
| Medium | 7 | 17 |
| Hard | 0 | 1 |

**Next problem:** 1789. Primary Department for Each Employee

---

## Daily Solutions

| Day | Problem | Difficulty | Category | Notes |
|:---:|:---|:---:|:---|:---:|
| 1 | 1757. Recyclable and Low Fat Products | Easy | Select | [View](./Day1/day1.md) |
| 2 | 584. Find Customer Referee | Easy | Select | [View](./Day2/day2.md) |
| 3 | 595. Big Countries | Easy | Select | [View](./Day3/day3.md) |
| 4 | 1148. Article Views I | Easy | Select | [View](./Day4/day4.md) |
| 5 | 1683. Invalid Tweets | Easy | Select | [View](./Day5/day5.md) |
| 6 | 1378. Replace Employee ID With The Unique Identifier | Easy | Basic Joins | [View](./Day6/day6.md) |
| 7 | 1068. Product Sales Analysis I | Easy | Basic Joins | [View](./Day7/day7.md) |
| 8 | 1581. Customer Who Visited but Did Not Make Any Transactions | Easy | Basic Joins | [View](./Day8/day8.md) |
| 9 | 197. Rising Temperature | Easy | Basic Joins | [View](./Day9/day9.md) |
| 10 | 1661. Average Time of Process per Machine | Easy | Basic Joins | [View](./Day10/day10.md) |
| 11 | 577. Employee Bonus | Easy | Basic Joins | [View](./Day11/day11.md) |
| 12 | 1280. Students and Examinations | Easy | Basic Joins | [View](./Day12/day12.md) |
| 13 | 570. Managers with at Least 5 Direct Reports | Medium | Basic Joins | [View](./Day13/day13.md) |
| 14 | 1934. Confirmation Rate | Medium | Basic Joins | [View](./Day14/day14.md) |
| 15 | 620. Not Boring Movies | Easy | Basic Aggregate Functions | [View](./Day15/day15.md) |
| 16 | 1251. Average Selling Price | Easy | Basic Aggregate Functions | [View](./Day16/day16.md) |
| 17 | 1075. Project Employees I | Easy | Basic Aggregate Functions | [View](./Day17/day17.md) |
| 18 | 1633. Percentage of Users Attended a Contest | Easy | Basic Aggregate Functions | [View](./Day18/day18.md) |
| 19 | 1211. Queries Quality and Percentage | Easy | Basic Aggregate Functions | [View](./Day19/day19.md) |
| 20 | 1193. Monthly Transactions I | Medium | Basic Aggregate Functions | [View](./Day20/day20.md) |
| 21 | 1174. Immediate Food Delivery II | Medium | Basic Aggregate Functions | [View](./Day21/day21.md) |
| 22 | 550. Game Play Analysis IV | Medium | Basic Aggregate Functions | [View](./Day22/day22.md) |
| 23 | 2356. Number of Unique Subjects Taught by Each Teacher | Easy | Sorting and Grouping | [View](./Day23/day23.md) |
| 24 | 1141. User Activity for the Past 30 Days I | Easy | Sorting and Grouping | [View](./Day24/day24.md) |
| 25 | 1070. Product Sales Analysis III | Medium | Sorting and Grouping | [View](./Day25/day25.md) |
| 26 | 596. Classes With at Least 5 Students | Easy | Sorting and Grouping | [View](./Day26/day26.md) |
| 27 | 1729. Find Followers Count | Easy | Sorting and Grouping | [View](./Day27/day27.md) |
| 28 | 619. Biggest Single Number | Easy | Sorting and Grouping | [View](./Day28/day28.md) |
| 29 | 1045. Customers Who Bought All Products | Medium | Sorting and Grouping | [View](./Day29/day29.md) |
| 30 | 1731. The Number of Employees Which Report to Each Employee | Easy | Advanced Select and Joins | [View](./Day30/day30.md) |

---

## Revise by Pattern

| Pattern | Practice with |
|:---|:---|
| Self join | [197](./Day9/day9.md), [570](./Day13/day13.md), [1731](./Day30/day30.md) |
| Finding missing matches | [1581](./Day8/day8.md), [577](./Day11/day11.md) |
| Keeping every combination | [1280](./Day12/day12.md) |
| Rates and percentages | [1934](./Day14/day14.md), [1633](./Day18/day18.md), [1211](./Day19/day19.md) |
| First event per group | [1070](./Day25/day25.md), [1174](./Day21/day21.md), [550](./Day22/day22.md) |
| Filtering groups | [596](./Day26/day26.md), [1045](./Day29/day29.md) |
| Counting unique values | [2356](./Day23/day23.md), [1141](./Day24/day24.md), [1045](./Day29/day29.md) |

---

## Full Problem List

### 01. Select
- [x] 1757. Recyclable and Low Fat Products
- [x] 584. Find Customer Referee
- [x] 595. Big Countries
- [x] 1148. Article Views I
- [x] 1683. Invalid Tweets

### 02. Basic Joins
- [x] 1378. Replace Employee ID With The Unique Identifier
- [x] 1068. Product Sales Analysis I
- [x] 1581. Customer Who Visited but Did Not Make Any Transactions
- [x] 197. Rising Temperature
- [x] 1661. Average Time of Process per Machine
- [x] 577. Employee Bonus
- [x] 1280. Students and Examinations
- [x] 570. Managers with at Least 5 Direct Reports
- [x] 1934. Confirmation Rate

### 03. Basic Aggregate Functions
- [x] 620. Not Boring Movies
- [x] 1251. Average Selling Price
- [x] 1075. Project Employees I
- [x] 1633. Percentage of Users Attended a Contest
- [x] 1211. Queries Quality and Percentage
- [x] 1193. Monthly Transactions I
- [x] 1174. Immediate Food Delivery II
- [x] 550. Game Play Analysis IV

### 04. Sorting and Grouping
- [x] 2356. Number of Unique Subjects Taught by Each Teacher
- [x] 1141. User Activity for the Past 30 Days I
- [x] 1070. Product Sales Analysis III
- [x] 596. Classes With at Least 5 Students
- [x] 1729. Find Followers Count
- [x] 619. Biggest Single Number
- [x] 1045. Customers Who Bought All Products

### 05. Advanced Select and Joins
- [x] 1731. The Number of Employees Which Report to Each Employee
- [ ] 1789. Primary Department for Each Employee
- [ ] 610. Triangle Judgement
- [ ] 180. Consecutive Numbers
- [ ] 1164. Product Price at a Given Date
- [ ] 1204. Last Person to Fit in the Bus
- [ ] 1907. Count Salary Categories

### 06. Subqueries
- [ ] 1978. Employees Whose Manager Left the Company
- [ ] 626. Exchange Seats
- [ ] 1341. Movie Rating
- [ ] 1321. Restaurant Growth
- [ ] 602. Friend Requests II: Who Has the Most Friends
- [ ] 585. Investments in 2016
- [ ] 185. Department Top Three Salaries

### 07. Advanced String Functions / Regex / Clause
- [ ] 1667. Fix Names in a Table
- [ ] 1527. Patients With a Condition
- [ ] 196. Delete Duplicate Emails
- [ ] 176. Second Highest Salary
- [ ] 1484. Group Sold Products By The Date
- [ ] 1327. List the Products Ordered in a Period
- [ ] 1517. Find Users With Valid E-Mails

---

## What Each Notes File Contains

The `dayN.md` files follow a common layout, so any problem can be revised quickly:

| Section | Purpose |
|:---|:---|
| Header | Difficulty, topic, date solved, runtime and status |
| Problem Statement | Table schema and the task, restated clearly |
| Real-Life Analogy | A simple picture to build intuition before writing SQL |
| Example Walkthrough | Input and output traced by hand |
| Step-by-Step Build | The query built up one clause at a time |
| Final Query | The accepted solution |
| Key Concepts | The SQL ideas the problem tests |
| Common Mistakes | Errors worth remembering |
| Interview Tips | How to recognize and explain this pattern |

---

## Repository Structure

```text
LeetCode-SQL-50-Solutions/
|-- README.md
|-- Day1/
|   |-- day1.md
|-- Day2/
|   |-- day2.md
|-- ...
|-- Day30/
    |-- day30.md
```

---

## Core SQL Concepts Covered

| Concept | Where it appears |
|:---|:---|
| `SELECT`, `WHERE`, filtering rows | Select |
| `JOIN` (inner, left) | Basic Joins |
| Self join | Basic Joins, Advanced Select and Joins |
| `GROUP BY` with `COUNT`, `SUM`, `AVG`, `MAX` | Basic Aggregate Functions, Sorting and Grouping, Advanced Select and Joins |
| `ROUND` | Basic Aggregate Functions, Advanced Select and Joins |
| `COUNT(DISTINCT ...)` | Sorting and Grouping |
| `HAVING` (filtering after grouping) | Sorting and Grouping |
| `ORDER BY`, `DISTINCT` | Sorting and Grouping |
| Subqueries in `FROM` (derived tables) | Sorting and Grouping |
| Subqueries in `HAVING` (compare a group with a total) | Sorting and Grouping |
| `NULL` handling with aggregates | Sorting and Grouping |

SQL logical execution order, used throughout the notes:

```text
FROM / JOIN -> WHERE -> GROUP BY -> HAVING -> SELECT -> ORDER BY -> LIMIT
```

---

## How to Use This Repository

1. Open the **Daily Solutions** table and pick a problem.
2. Read the notes file for that day, up to the Step-by-Step Build section.
3. Try to write the query yourself on LeetCode before looking at the final query.
4. Compare your query with the accepted one and read the Common Mistakes section.
5. Use **Revise by Pattern** to practise similar problems together.

---

## Author

**Arpan Chakraborty**
GitHub: [ArpanC6](https://github.com/ArpanC6)

If this repository helped you, a star is appreciated.