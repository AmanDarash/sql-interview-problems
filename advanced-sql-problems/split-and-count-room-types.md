# Split and Count Room Type Searches

## Problem

We have a table `airbnb_searches` that stores the room types users searched for.
However, the `filter_room_types` column can contain **multiple room types separated by commas**.

We need to determine **how many times each room type was searched**.

### Table: airbnb_searches

| user_id | date_searched | filter_room_types |
|-------|--------------|------------------|
| 1 | 2022-01-01 | entire home, private room |
| 2 | 2022-01-02 | entire home, shared room |
| 3 | 2022-01-02 | private room, shared room |
| 4 | 2022-01-03 | private room |

### Requirement

1. Split the `filter_room_types` column into individual room types.
2. Treat each room type as a separate row.
3. Count how many times each room type appears.
4. Sort the results in descending order of search count.

### Expected Output

| value | cnt |
|------|-----|
| private room | 3 |
| shared room | 2 |
| entire home | 2 |

---

# SQL Solution

```sql
SELECT 
    LTRIM(RTRIM(value)) AS value,
    COUNT(*) AS cnt
FROM airbnb_searches
CROSS APPLY STRING_SPLIT(filter_room_types, ',')
GROUP BY LTRIM(RTRIM(value))
ORDER BY cnt DESC;
