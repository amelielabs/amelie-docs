---
weight: 5
title: ARRAY
type: docs
bookToc: false
---

## ARRAY

Unary square brackets **`[]`** operator can be used to create an array object. Arrays can have zero or
more values. Index operator **`[`** can be used to access array value by index.
Array can contain values of any other type.

Table rows are stored as arrays.

[Array Functions](/docs/sql/functions/array) are designed to do basic operations using arrays.

---

```SQL
select [1,2,3]
[1,2,3]

select [1,2,3]::append(4)
[1,2,3,4]

select ["a", null, {}]
["a", null, {}]

select [1, "a", {"id": 48}]
[1, "a", {
  "id": 48
}]

select []
[]

select * from [1,2,3]
[1, 2, 3]
```

```SQL
create table test (id int primary key, data array)
insert into test values (1, [1,2,3]), (2, ['a', 'b', 'c'])

select * from test
[[1, [1, 2, 3]], [2, ["a", "b", "c"]]]

select data from test
[[1, 2, 3], ["a", "b", "c"]]

update test set data = data::append(4) where id = 1
```
