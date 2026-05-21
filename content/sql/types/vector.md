---
weight: 13
title: VECTOR
type: docs
bookToc: true
---

# VECTOR

**`VECTOR`** type represents an array of floats and is optimized for fast float operations.

Vector values must be integers or floats. Vectors can be compared, added together,
subtracted, multiplied, or divided.

---

```SQL
SELECT vector [1,2,3] as const;

const
─────
[1, 2, 3]

select [1,2,3]::vector;

vector
──────
[1, 2, 3]

SELECT [3,2,0,1,4]::vector::cos_distance([1,3,1,2,0]::vector);

cos_distance
────────────
0.481455
```

```SQL
-- similarity vector search
CREATE TABLE example (id serial primary key, embedding vector);
INSERT INTO example (embedding) values ([3,2,0,1,4]);
INSERT INTO example (embedding) values ([2,2,0,1,3]);
INSERT INTO example (embedding) values ([1,3,0,1,4]);
SELECT * FROM example;

id  embedding
─────────────────────
0   [3, 2, 0, 1, 4]
1   [2, 2, 0, 1, 3]
2   [1, 3, 0, 1, 4]

-- order rows by similarity
SELECT
   id, embedding::cos_distance(vector [1,3,1,2,0])
FROM
   example
ORDER BY 2 desc;

id  cos_distance
──────────────────
0   0.481455
2   0.403715
1   0.391419
```
