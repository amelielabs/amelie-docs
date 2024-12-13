---
weight: 3
title: UPDATE
type: docs
bookToc: false
---

## UPDATE Statement

```SQL
UPDATE [schema.]table_name SET column[.path] = expr | DEFAULT [, ... ] 
[WHERE expr]
[RETURNING expr [AS alias][, ...] [FORMAT type]]
```

Update rows in the table.

The Update operation is distributed and will transactionally update table partitions on one or more nodes.
Update can be part of a multi-statement transaction.

If the table schema is not defined, the table name will be searched in the **`public`** schema.

The **`RETURNING`** clause allows the values to be returned in case of successful completion. The values can
be used as a result in the corresponding [CTE](/docs/sql/transactions/cte) or as a standalone result.

The [FORMAT](/docs/sql/query/format) clause can be used to specify the format of the result.

---

```SQL
create table example (id int primary key, data json);
insert into example values (1, [1,2,3]), (2, ['a', 'b', 'c']);

select data from example;
[[1, 2, 3], ["a", "b", "c"]]

update example set data = data::append(4) where id = 1 returning *;
[[1, [1, 2, 3, 4]]]
```

```SQL
create table example (id int primary key, obj json);
insert into example values (1, {"id": 1, "data": null});

update example set obj.data = [1,2,3] returning *;
[[1, {
  "id": 1,
  "data": [1, 2, 3]
}]]

update example set obj.data = obj.data::append(4) returning *;
[[1, {
  "id": 1,
  "data": [1, 2, 3, 4]
}]]
```

```SQL
-- with CTE
with updated_items as (
    update example set data = data::append(4) where id = 1 returning *
) select count(*) from updated_items;
[1]
```
