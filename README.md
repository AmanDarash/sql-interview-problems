# 📊 Advanced SQL Practice Repository

## 🚀 Overview

This repository contains structured solutions to advanced SQL problems.

It focuses on strengthening:

- Window functions  
- Aggregations  
- Joins  
- Subqueries  
- Ranking logic  
- Date and string functions  
- Query optimization basics  

The purpose is to build strong SQL fundamentals through practice and clear explanations.

---

## 🧩 Example Problem

### Problem  
Find the top 3 employees by salary in each department.

### Solution (MySQL)

```sql
SELECT emp_id, dept_id, salary
FROM (
    SELECT emp_id,
           dept_id,
           salary,
           DENSE_RANK() OVER (
               PARTITION BY dept_id
               ORDER BY salary DESC
           ) AS rnk
    FROM employees
) t
WHERE rnk <= 3;
```
## Explanation

- DENSE_RANK() assigns ranks without gaps when there are ties.

- PARTITION BY dept_id groups employees within each department.

- ORDER BY salary DESC ranks employees by highest salary first.

- The outer query filters the top 3 ranked employees per department.

## 📂 Repository Structure
```.
├── README.md
├── Functions.md
├── Lessons-Learned.md
├── Cheatsheet.md
└── problems/
```

## 📘 Files Description
### Functions.md

Detailed explanations of SQL functions such as:

- RANK

- DENSE_RANK

- ROW_NUMBER

- CASE

- COALESCE

- Date functions

### Lessons-Learned.md

Covers:

- Common SQL mistakes

- NULL handling

- GROUP BY pitfalls

- Practical observations

### Cheatsheet.md

Quick syntax reference across:

- MySQL

- Oracle

- SQL Server

- problems/

Collection of SQL practice problems with structured solutions.

## 🎯 Purpose

This repository is created to:

- Improve SQL problem-solving skills

- Practice advanced query patterns

- Maintain structured notes for revision

- Build consistent technical documentation habits

## 🛠 SQL Variants Covered

- MySQL

- Oracle

- SQL Server

- ANSI SQL concepts

## 📌 Note

This repository is part of continuous technical learning and improvement.
