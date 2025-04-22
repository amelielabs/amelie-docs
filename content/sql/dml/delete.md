---
weight: 4
title: DELETE
type: docs
bookToc: false
---

## DELETE Statement

```SQL
[WITH cte_name ...]
DELETE FROM [schema.]table_name
[WHERE expr]
[RETURNING expr [AS alias][, ...] [FORMAT type]]
```

Delete rows in the table.

The Delete operation is distributed and will transactionally update table partitions on one or more backends.
Delete can be part of a multi-statement transaction.

If the table schema is not defined, the table name will be searched in the **`public`** schema.

The **`RETURNING`** clause allows the values to be returned in case of successful completion. The values can
be used as a result in the corresponding [CTE](/docs/sql/cte) or as a standalone result.

The [FORMAT](/docs/sql/query/format) clause can be used to specify the format of the result.

---

```SQL
create table example (id int primary key, data json);
insert into example values (1, [1,2,3]), (2, ['a', 'b', 'c']);
delete from example;

select count(*) from example;
[0]
```

```SQL
-- with CTE
with deleted_items as (
    delete from example returning *
) select count(*) from deleted_items;
[3]
```
