# Evaluating Formula Values from a Table

## Problem

You are given a table `Input` containing three columns:

- `id`
- `formula`
- `value`

Some rows contain a direct numeric value, while others contain a formula referencing other rows.

The formula format is simple:

<ID><operator><ID>

Example formulas:

A+B  
B-A

Where:
- `A` and `B` refer to rows in the same table
- `+` or `-` is the operator

Your task is to evaluate the formula and compute the resulting value.

---

## Table Structure

| id | formula | value |
|----|--------|------|
| A | NULL | 10 |
| B | NULL | 20 |
| C | A+B | NULL |
| D | B-A | NULL |

---

## Expected Output

| id | formula | operator | value1 | value2 | new_value |
|----|--------|----------|--------|--------|----------|
| C | A+B | + | 10 | 20 | 30 |
| D | B-A | - | 20 | 10 | 10 |

---

## SQL Solution

```sql
WITH CTE AS (
    SELECT 
        id,
        formula,
        value,
        LEFT(formula,1) AS id1,
        RIGHT(formula,1) AS id2,
        SUBSTRING(formula,2,1) AS op
    FROM Input
)

SELECT 
    c.id,
    c.formula,
    c.op,
    i1.value AS value1,
    i2.value AS value2,
    CASE
        WHEN c.op = '+' THEN i1.value + i2.value
        ELSE i1.value - i2.value
    END AS new_value
FROM CTE c
INNER JOIN Input i1 
    ON c.id1 = i1.id
INNER JOIN Input i2 
    ON c.id2 = i2.id;
```

---

## Explanation

### Step 1: Parse the Formula

We extract parts of the formula using string functions:

- `LEFT(formula,1)` → first operand
- `RIGHT(formula,1)` → second operand
- `SUBSTRING(formula,2,1)` → operator

Example:

| formula | id1 | op | id2 |
|-------|----|----|----|
| A+B | A | + | B |
| B-A | B | - | A |

---

### Step 2: Join Back to the Table

We join the extracted IDs back to the `Input` table to retrieve their numeric values.

Example after join:

| id | value1 | value2 |
|----|-------|-------|
| C | 10 | 20 |
| D | 20 | 10 |

---

### Step 3: Calculate Result

Using a `CASE` expression:

A+B → value1 + value2  
B-A → value1 - value2

---

## SQL Concepts Demonstrated

- Common Table Expressions (CTE)
- String parsing using `LEFT`, `RIGHT`, and `SUBSTRING`
- Self joins
- Conditional logic using `CASE`

---

## Real-World Use Case

This type of logic is useful when working with:

- derived metrics
- rule-based calculations
- financial formula evaluation
- dynamic computation tables
