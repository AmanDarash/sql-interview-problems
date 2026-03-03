# 🚀 Advanced SQL Problems

This folder contains solutions to complex SQL problems that require strong understanding of window functions, subqueries, analytical functions, and performance-aware query design.

These problems are designed to strengthen problem-solving ability and improve query structuring skills.

---

## 📌 Topics Covered

- Window Functions (`RANK`, `DENSE_RANK`, `ROW_NUMBER`)
- Analytical Functions
- Correlated Subqueries
- Complex Joins
- Grouping & Aggregation Edge Cases
- Conditional Logic (`CASE`)
- Date & String Manipulation
- Performance-Oriented Query Design

---

## 🧠 Approach

Each problem includes:

- Clear problem statement  
- Structured SQL solution  
- Explanation of logic  
- Notes on edge cases (if applicable)  

The goal is not just to solve the problem, but to understand:

- Why the solution works  
- Alternative approaches  
- When to use specific SQL functions  

---

## 🛠 Example Pattern Used

Many advanced problems use window functions like:

```sql
SELECT *,
       DENSE_RANK() OVER (PARTITION BY column_name ORDER BY value DESC) AS rnk
FROM table_name;
