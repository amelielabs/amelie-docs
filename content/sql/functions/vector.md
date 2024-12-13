---
weight: 7
title: "Vector"
bookToc: false
---

## Vector Functions

All vector functions are located in the **`public`** schema, which is default.

---

### **`vector vector(json)`**

Convert from **`JSON`** array to **`VECTOR`**. Array values must be integers or floats.

```SQL
select [1.0, 2.1, 3]::vector * [1.5, 1.5, 1.5]::vector;
[1.5, 3.15, 4.5]
```

---

### **`vector cos_distance(vector, vector)`**

Calculate cosine distance between two vectors.

```SQL
select [3,2,0,1,4]::vector::cos_distance([1,3,1,2,0]::vector);
[0.481455]
```

```SQL
create table example (id int primary key serial, embedding vector);
insert into example (embedding) values ([3,2,0,1,4]);
insert into example (embedding) values ([2,2,0,1,3]);
insert into example (embedding) values ([1,3,0,1,4]);
select * from example;
[[0, [3, 2, 0, 1, 4]], [1, [2, 2, 0, 1, 3]], [2, [1, 3, 0, 1, 4]]]

-- order rows by similarity
select id, embedding::cos_distance(vector [1,3,1,2,0])
from example
order by 2 desc;
[[0, 0.481455], [2, 0.403715], [1, 0.391419]]

-- find the most alike row
select id from example
order by embedding::cos_distance(vector [1,3,1,2,0]) desc
limit 1;
[0]
```
