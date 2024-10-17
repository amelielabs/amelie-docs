---
weight: 4
title: DELETE
type: docs
bookToc: false
---

## DELETE Statement

```SQL
DELETE FROM [schema.]table_name
[WHERE expr]
[RETURNING expr [INTO cte]]
```

Delete rows in the table.

The Delete operation is distributed and will transactionally update table partitions on one or more nodes.
Delete can be part of a multi-statement transaction.

If the table schema is not defined, the table name will be searched in the **`public`** schema.

The **`RETURNING`** clause allows the defined expression value to be returned in case of successful completion. This value can
be used as a result in the corresponding [CTE](/docs/sql/transactions/cte) or as a standalone result.

The **`INTO`** clause provides an alternative way to define this statement as a [CTE](/docs/sql/transactions/cte).

---

```SQL
create table test (id int primary key, data array)
insert into test values (1, [1,2,3]), (2, ['a', 'b', 'c'])
delete from test

select count(*) from test
[0]
```

```SQL
-- with CTE
with deleted_items as (
    delete from test returning *
) select count(*) from deleted_items;
[3]

-- alternative CTE form using RETURNING INTO
begin;
delete from test returning * into deleted_items;
select count(*) from deleted_items;
commit;
[3]

begin;
delete from test returning * into deleted_items;
select deleted_items::size
commit;
[3]
```
