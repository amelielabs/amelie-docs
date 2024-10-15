---
weight: 6
title: OBJECT
type: docs
bookToc: false
---

## OBJECT

Defines a JSON object. The types **`OBJ`** and **`OBJECT`** are synonymous.

Unary curly brackets **`{}`** operator can be used to create an object. An object can have zero or more values.
Each value must have a unique key. The dot operator **`.`** and index operator **`[`** can access the object
value by key.

Objects are dynamic, and each value is an expression that is evaluated at runtime.
It may contain other expressions, function calls, and subqueries.

[Object Functions](/docs/sql/functions/object) are designed to do basic operations using objects.

---

```SQL
select {"id": 48, "data": [1,2,3]}
[{
  "id": 48,
  "data": [1, 2, 3]
}]

select {"id": 48, "data": [1,2,3]}.id
[48]

select {"id": 48, "data": [1,2,3]}.data[0]
[1]

select {"id": 48, "data": [1,2,3]}."data"[0]
[1]

select {"id": 48, "data": [1,2,3]}["data"][0]
[1]

select {"at": current_timestamp, "id": system.config().uuid}
[{
  "at": "2024-09-26 16:14:00.722393+03",
  "id": "a74fbf39-cc9d-314e-a33e-3aa47559ffe5"
}]

select {"list": select * from [1,2,3]}
[{
  "list": [1, 2, 3]
}]

select id from [{'id': 1}, {'id': 2}]
[1, 2]

select * from {"a": 1, "b": 2}
[1, 2]

select ** from {"a": 1, "b": 2}
["a", "b"]
```

```SQL
create table test (id int primary key, data object)
insert into test values (1, {"id": 48, "metrics": [1,2,3]})

select * from test
[[1, {
  "id": 48,
  "metrics": [1, 2, 3]
}]]

select data.metrics[0] from test
[1]

select (select sum(*) from test.data.data) from test;
[[6]]

update test set data.new_field = data.id

select data from test
[{
  "id": 48,
  "data": [1, 2, 3],
  "new_field": 48
}]

```

```SQL
create table schemaless (obj object, primary key (obj.id int))
insert into schemaless {"id": 48, "data": [1,2,3]}

select obj from schemaless
[{
  "id": 48,
  "data": [1, 2, 3]
}]
```
