---
weight: 12
title: VECTOR
type: docs
bookToc: false
---

## VECTOR

**`VECTOR`** type represents an array of floats and is optimized for fast float operations.

Vector values must be integers or floats. Vectors can be compared, added together,
subtracted, multiplied, or divided.

---

```SQL
select vector [1,2,3];
[1, 2, 3]

select [1,2,3]::vector;
[1, 2, 3]

select [1.0, 2.1, 3]::vector * [1.5, 1.5, 1.5]::vector;
[1.5, 3.15, 4.5]

select [3,2,0,1,4]::vector::cos_distance([1,3,1,2,0]::vector);
[0.481455]
```

```SQL
-- similarity search
create table example (id int primary key serial, embedding vector);
insert into example (embedding) values ([3,2,0,1,4]);
insert into example (embedding) values ([2,2,0,1,3]);
insert into example (embedding) values ([1,3,0,1,4]);
select * from example;
[[1, [3, 2, 0, 1, 4]], [2, [2, 2, 0, 1, 3]], [3, [1, 3, 0, 1, 4]]]

-- order rows by similarity
select
   id, embedding::cos_distance(vector [1,3,1,2,0])
from
   example
order by 2 desc;
[[1, 0.481455], [3, 0.403715], [2, 0.391419]]
```
