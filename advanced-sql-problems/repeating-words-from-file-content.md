# Finding Repeating Words in File Content

## Problem

You are given a table containing a file name and its content.  
The content column contains multiple words separated by spaces.

Your task is to **identify the words that appear more than once** across the dataset.

---

## Table Structure

Table: `namaste_python`

| file_name | content |
|-----------|---------|
| file1 | hello world hello |
| file2 | sql python sql data |

---

## Requirement

1. Split the content into individual words.
2. Treat each word as a separate row.
3. Count how many times each word appears.
4. Return only the words that appear **more than once**.

---

## Expected Output

| value | cnt |
|------|-----|
| hello | 2 |
| sql | 2 |

---

## SQL Solution

```sql
SELECT s.value, COUNT(*) AS cnt
FROM namaste_python
CROSS APPLY STRING_SPLIT(content,' ') AS s
GROUP BY s.value
HAVING COUNT(*) > 1;
