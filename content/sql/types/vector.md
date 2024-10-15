---
weight: 10
title: VECTOR
type: docs
bookToc: false
---

## VECTOR

Vector is identical to an array but optimized for fast float operations.

Vector values must be integers or reals. Vectors can be compared, added together,
subtracted, multiplied, or divided.

---

```SQL
select [1,2,3]::vector
[1, 2, 3]

select [1.0, 2.1, 3]::vector * [1.5, 1.5, 1.5]::vector
[1.5, 3.15, 4.5]

select [3,2,0,1,4]::vector::cos_distance([1,3,1,2,0]::vector)
[0.481455]
```

```SQL
create table test (id int primary key serial, embedding vector)
insert into test (embedding) values (vector [3,2,0,1,4])

select * from test
[[0, [3, 2, 0, 1, 4]]]

select type(embbeding) from test
["vector"]

select embedding::cos_distance([1,3,1,2,0]::vector) from test
[0.481455]
```
