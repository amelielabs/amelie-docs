---
weight: 6
title: JSON
type: docs
bookToc: false
---

## JSON Expressions

Unary square brackets **`[]`** operator can be used to create an array object. Arrays can have zero or
more values. Index operator **`[`** can be used to access array value by index.
Array can contain values of any other type.

Unary curly brackets **`{}`** operator can be used to create an object. An object can have zero or more values.
Each value expected to have a unique key, but this is not enforced. The dot operator **`.`** and index
operator **`[`** can access the object value by key.

Objects are dynamic, and each value is an expression that is evaluated at runtime.
It may contain other expressions, function calls, and subqueries.

[JSON Functions](/docs/sql/functions/json) can be used to do basic operations using JSON arrays and objects.

Any type can be [casted](/docs/sql/functions/casting) to the **`JSON`**, or a string can be
parsed and [imported](/docs/sql/functions/json) as the **`JSON`** type.

---

```SQL
select [1,2,3];
[1, 2, 3]

select [1,2,3][2];
[3]

select {"id": 48, "data": [1,2,3]};
[{
  "id": 48,
  "data": [1, 2, 3]
}]

select {"id": 48, "data": [1,2,3]}.data[0];
[1]

select {"at": current_timestamp, "id": system.config().uuid};
[{
  "at": "2024-09-26 16:14:00.722393+03",
  "id": "a74fbf39-cc9d-314e-a33e-3aa47559ffe5"
}]

select {"total": select count(*) from test};
[{
  "total": 3
}]
```
