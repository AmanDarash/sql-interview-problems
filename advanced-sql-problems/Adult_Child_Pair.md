
## Problem: Pair Adults and Children

We have a table **People** with the following structure:
```

| Person | Type  |
|------|------|
| A1 | Adult |
| A2 | Adult |
| A3 | Adult |
| A4 | Adult |
| A5 | Adult |
| C1 | Child |
| C2 | Child |
| C3 | Child |
| C4 | Child |
```

### Requirement

Each **child must be paired with exactly one adult**, but **an adult can remain unpaired** if there are more adults than children.

Children **cannot appear alone** in the result.

### Expected Output
```

| Adult | Child |
|------|------|
| A1 | C1 |
| A2 | C2 |
| A3 | C3 |
| A4 | C4 |
| A5 | NULL |

```

### Notes

- Every child must have an associated adult.
- If there are extra adults, they should appear with `NULL` as the child.
- The solution should use SQL logic to pair rows appropriately.

## My Code
```sql
select adult,child from 
(select Person as child,row_number() over(order by Person) as rw_num from People where Type='Child') as c
right join
(Select Person as adult,row_number() over(order by Person) as rw_num from People where Type='Adult') as a
on c.rw_num=a.rw_num
```
