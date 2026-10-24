# 595. Big Countries

**Difficulty:** Easy
**Topic:** Select / Basic Filtering
**LeetCode:** https://leetcode.com/problems/big-countries/
**Solved on:** 9/10/2026
**Runtime:** 297 ms (Beats 73.07%)
**Status:** Accepted (7/7 testcases passed)

---


## Problem Statement

**Table:** `World`

| Column Name | Type    | Description |
|-------------|---------|-------------|
| name        | varchar | Primary Key (country name) |
| continent   | varchar | Continent name |
| area        | int     | Area in km² |
| population  | int     | Population count |
| gdp         | bigint  | GDP value |

Each row gives information about the name of a country, the continent, its area, population, and GDP value.

### Task
A country is **big** if:
- It has an area of **at least 3,000,000** (area >= 3000000), OR
- It has a population of **at least 25,000,000** (population >= 25000000)

Find the `name`, `population`, and `area` of the big countries.

Return result in any order.

---

## Understanding the Problem

I need to find all **big countries**. Big means:
1. Area **at least 3,000,000** -> `area >= 3000000`
2. **OR** population **at least 25,000,000** -> `population >= 25000000`

Either one is enough, so I use **OR**.

Output needs: `name`, `population`, `area` (3 columns).

---

## Example Walkthrough

### Input Table (World)

| name        | continent | area    | population | gdp          |
|-------------|-----------|---------|------------|--------------|
| Afghanistan | Asia      | 652230  | 25500100   | 20343000000  |
| Albania     | Europe    | 28748   | 2831741    | 12960000000  |
| Algeria     | Africa    | 2381741 | 37100000   | 188681000000 |
| Andorra     | Europe    | 468     | 78115      | 3712000000   |
| Angola      | Africa    | 1246700 | 20609294   | 100990000000 |

### Step 1: Check area >= 3000000

| name        | area    | >= 3M?  |
|-------------|---------|---------|
| Afghanistan | 652230  | NO      |
| Albania     | 28748   | NO      |
| Algeria     | 2381741 | NO      |
| Andorra     | 468     | NO      |
| Angola      | 1246700 | NO      |

No country has area greater than 3M.

### Step 2: Check population >= 25000000

| name        | population | >= 25M? |
|-------------|------------|---------|
| Afghanistan | 25500100   | YES     |
| Albania     | 2831741    | NO      |
| Algeria     | 37100000   | YES     |
| Andorra     | 78115      | NO      |
| Angola      | 20609294   | NO      |

### Step 3: Combine with OR

| name        | area >= 3M? | pop >= 25M? | OR Result |
|-------------|-------------|-------------|-----------|
| Afghanistan | NO          | YES         | YES       |
| Albania     | NO          | NO          | NO        |
| Algeria     | NO          | YES         | YES       |
| Andorra     | NO          | NO          | NO        |
| Angola      | NO          | NO          | NO        |

### Output

| name        | population | area    |
|-------------|------------|---------|
| Afghanistan | 25500100   | 652230  |
| Algeria     | 37100000   | 2381741 |

Order can be any.

---

## Final Query

```sql
SELECT name, population, area
FROM World
WHERE area >= 3000000 OR population >= 25000000;