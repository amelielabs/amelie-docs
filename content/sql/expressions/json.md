---
weight: 6
title: JSON
type: docs
bookToc: false
---

## JSON Expressions

Unary square brackets **`[]`** operator can be used to create an array object. Arrays can have zero or
more values. Index operator **`[`** can be used to access array value by index.

[Array Functions](/docs/sql/functions/array) are designed to do basic operations using arrays.

Unary curly brackets **`{}`** operator can be used to create an object. An object can have zero or more values.
Each value must have a unique key. The dot operator **`.`** and index operator **`[`** can access the object
value by key.

[Object Functions](/docs/sql/functions/object) are designed to do basic operations using objects.

Both array and object can contain values of any other type. Arrays and objects are dynamic, and
each value is an expression evaluated at runtime. It may contain other expressions, function
calls, and subqueries.

---

```SQL
select [1,2,3]
[1, 2, 3]

select [1,2,3][2]
[3]

select * from [1,2,3]
[1, 2, 3]

select {"id": 48, "data": [1,2,3]}
[{
  "id": 48,
  "data": [1, 2, 3]
}]

select {"id": 48, "data": [1,2,3]}.data[0]
[1]

select {"at": current_timestamp, "id": system.config().uuid}
[{
  "at": "2024-09-26 16:14:00.722393+03",
  "id": "a74fbf39-cc9d-314e-a33e-3aa47559ffe5"
}]

select {"total": select count(*) from [1,2,3]}
[{
  "total": [3]
}]
```
