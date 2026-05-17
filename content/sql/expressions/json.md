---
weight: 6
title: JSON
type: docs
bookToc: true
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

[JSON Functions](/docs/sql/builtin/json) can be used to do basic operations using JSON arrays and objects.

Any type can be [casted](/docs/sql/builtin/casting) to the **`JSON`**, or a string can be
parsed and [imported](/docs/sql/builtin/json) as the **`JSON`** type.

---

```SQL
SELECT [1,2,3] as const;

const
─────
[1, 2, 3]

SELECT [1,2,3][2] as expr;

expr
────
3

SELECT {"id": 48, "data": [1,2,3]} as json;

json
────
{
  "id": 48,
  "data": [1, 2, 3]
}

SELECT {"id": 48, "data": [1,2,3]}.data[0] as json_expr;

json_expr
─────────
1

SELECT {"at": current_timestamp, "id": show('config').uuid} as json_expr;

json_expr
─────────
{
  "at": "2026-05-17 17:59:01.821945+03",
  "id": "b9b6fbf1-85de-9a0b-63e2-3233e03c6803"
}

SELECT
{
  "total": select count(*) from test
} as json_expr;

json_expr
─────────
{
  "total": 3
}
