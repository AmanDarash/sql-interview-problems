# Compare Source and Target Tables

## Problem

You are given two tables: **Source** and **Target**.

Your task is to compare the records in both tables and return only the **differences**.

The output should identify:

- Records that exist in **Target but not in Source** → `New in Target`
- Records that exist in **Source but not in Target** → `New in Source`
- Records where the **ID exists in both tables but other columns differ** → `Mismatch`

Rows that match exactly in both tables should **not appear in the result**.

---

## Table Structure

### Source

| id | Name |
|----|------|
| 1  | John |
| 2  | Alex |
| 3  | Mary |

### Target

| id | Name |
|----|------|
| 1  | John |
| 2  | David |
| 4  | Sam |

---

## Expected Output

| ID | Status |
|----|--------|
| 2  | Mismatch |
| 3  | New in Source |
| 4  | New in Target |

---

## SQL Solution

```sql
SELECT 
    COALESCE(t.id, s.id) AS ID,
    CASE
        WHEN s.id IS NULL THEN 'New in Target'
        WHEN t.id IS NULL THEN 'New in Source'
        WHEN s.Name <> t.Name THEN 'Mismatch'
    END AS Status
FROM Source s
FULL OUTER JOIN Target t
    ON s.id = t.id
WHERE 
    s.id IS NULL
    OR t.id IS NULL
    OR s.Name <> t.Name;
