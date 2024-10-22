---
weight: 2
title: INSERT / UPSERT
type: docs
bookToc: false
---

## INSERT Statement


```SQL
INSERT INTO [schema.]table_name [(column[, ...])]
VALUES (expr[, ...])[, ...] | expr[, ...]
[ON CONFLICT DO NOTHING | UPDATE ...]
[RETURNING expr [INTO cte]]
```

Insert one or more rows into the table.

The Insert operation is distributed and will transactionally update table partitions on one or more nodes.
Insert can be part of a multi-statement transaction.

If the table schema is not defined, the table name will be searched in the **`public`** schema.

If the column list is not defined, all values must correspond to the table column types. If the column list is
defined, only the list-defined columns will be set to the corresponding values. Non-defined column values will be
set to **`NULL`**, **`SERIAL`** value or **`DEFAULT`** constraint value will be used (if defined).
If more than one **`SERIAL`** columns are used, they will share the same value.

If the table column has only one column, the **`VALUES`** clause can be omitted, and the column value
can be provided as an expression.

If the row already exists (according to the primary key), the table primary index unique constraint violation error
will be emitted. The **`ON CONFLICT`** clause allows to change this behavior by providing the following options:

* **`DO NOTHING`**

  If the key already exists, ignore the operation.

* **`UPDATE`**

  If the key already exists, apply the **`UPDATE`** statement on the existing key.

The **`RETURNING`** clause allows the defined expression value to be returned in case of successful completion. This value can
be used as a result in the corresponding [CTE](/docs/sql/transactions/cte) or as a standalone result.

The **`INTO`** clause provides an alternative way to define this statement as a [CTE](/docs/sql/transactions/cte).

### Data Ingestion and Streaming

An alternative way to insert different formats directly into a table without using **`SQL`** is to use the
[HTTP API](/docs/api/overview).

---

```SQL
create table test (id int primary key, matches int)
insert into test values (1, 0) on conflict do update set matches = matches + 1
insert into test values (1, 0) on conflict do update set matches = matches + 1
insert into test values (1, 0) on conflict do update set matches = matches + 1
select * from test
[[1, 2]]
```

```SQL
create table test (device int primary key, metrics array)
insert into test values (48, [1,2,3]), (56, [3,1])
select * from test
[[48, [1, 2, 3]], [56, [3, 1]]]
```

```SQL
create table test (id int primary key serial, obj object)

insert into test (obj) values ({"metrics": [1,2,3]})
insert into test (obj) values ({"metrics": [1,2,3]})

select * from test
[[0, {
  "metrics": [1, 2, 3]
}], [1, {
  "metrics": [1, 2, 3]
}]]
```

```SQL
create table test (obj object, primary key (obj.id int))
insert into test {"id": 48, "metrics": [1,2,3]}, {"id": 56}

select obj from test where obj::has("metrics")
[{
  "id": 48,
  "metrics": [1, 2, 3]
}]
```

```SQL
-- with CTE
with inserted_items as (
    insert into test values (1), (2), (3) returning *
) select count(*) from inserted_items;
[3]

-- alternative CTE form using RETURNING INTO
begin;
insert into test values (1), (2), (3) returning * into inserted_items;
select count(*) from inserted_items;
commit;
[3]
```
