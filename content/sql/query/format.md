---
weight: 2
title: "FORMAT"
bookToc: false
---

## FORMAT Clause

```SQL
FORMAT '<type>[-modifier [...]]'

SELECT expr, ... [FORMAT 'type']
RETURNING expr, ... [FORMAT 'type']
```

The **`FORMAT`** clause can specify result formatting and set the **`Content-Type`**.

The **`FORMAT`** clause can be specified for the [SELECT](/docs/sql/query/select) statement and [RETURNING](/docs/sql/transactions/cte) clause used by all DML Statements.
Format string can have zero or more modifiers, each separated with a **`-`** symbol.
Modifiers can be defined in any order.

The **`format`** config variable specifies the default format.

Currently, the following format types are supported:

---

## **`json (application/json)`**

| Modifier       |  Description |
| :---------------- |  :----       |
|  array            | Encode results using JSON and an array for rows. Column names will be omitted (Default). |
|  obj              | Encode the result using JSON using an object for rows; each key will have a column name. |
|  pretty           | Apply formatting for a more manageable read. |


```SQL
select {"id": 1, "data": [1,2,3]} as result format 'json';
[{"id": 1, "data": [1, 2, 3]}]

select {"id": 1, "data": [1,2,3]} as result format 'json-pretty';
[{
  "id": 1,
  "data": [1, 2, 3]
}]

select {"id": 1, "data": [1,2,3]} as result format 'json-obj';
[{"result": {"id": 1, "data": [1, 2, 3]}}]

select {"id": 1, "data": [1,2,3]} as result format 'json-obj-pretty';
[{
  "result": {
    "id": 1,
    "data": [1, 2, 3]
  }
}]

insert into test values (1), (2), (3) returning * format 'json-array'
[1, 2, 3]

insert into test values (1), (2), (3) returning * format 'json-obj';
[{"id": 1}, {"id": 2}, {"id": 3}]

show format
["json-pretty"]

```
