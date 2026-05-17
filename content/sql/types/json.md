---
weight: 9
title: JSON
type: docs
bookToc: true
---

## JSON

**`JSON`** type is a binary representation of the [JSON](https://www.json.org/) (JavaScript Object Notation).
It can be used as a column type or as a part of a expression using the **`[]`** and
**`{}`** operators.

Unary square brackets **`[]`** operator can be used to create an array object. Arrays can have zero or
more values. Index operator **`[`** can be used to access array value by index.
Array can contain values of any other type.

Unary curly brackets **`{}`** operator can be used to create an object. An object can have zero or more values.
Each value expected to have a unique key, but this is not enforced. The dot operator **`.`** and index
operator **`[`** can access the object value by key.

Objects are dynamic, and each value is an expression that is evaluated at runtime.
It may contain other expressions, function calls, and subqueries.

[JSON Functions](/docs/sql/builtin/json) can be used to do basic operations using JSON arrays and objects.

Any type can be [casted](/docs/sql/builtin/casting) to the **`JSON`**, or a string can be
parsed and [imported](/docs/sql/builtin/json) as the **`JSON`** type.

---

```SQL
SELECT [1,2,3] as example;

example
───────
[1, 2, 3]

SELECT [1,2,3]::append(4);

append
──────
[1,2,3,4]

SELECT {"id": 48, "data": [1,2,3]} as example;

example
───────
{
  "id": 48,
  "data": [1, 2, 3]
}

SELECT {"id": 48, "data": [1,2,3]}.data[0] as data;

data
────
1

SELECT {"at": current_timestamp, "id": show().uuid} as json;

json
────
{
  "at": "2026-05-17 17:08:19.596411+03",
  "id": "b9b6fbf1-85de-9a0b-63e2-3233e03c6803"
}
```

```SQL
CREATE TABLE example (id int primary key, metrics json);
```
