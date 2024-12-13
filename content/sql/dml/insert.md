---
weight: 2
title: INSERT / UPSERT
type: docs
bookToc: false
---

## INSERT Statement


```SQL
[WITH cte_name ...]
INSERT INTO [schema.]table_name [(column[, ...])]
VALUES (value[, ...])[, ...]
[ON CONFLICT DO NOTHING | ERROR | RESOLVE | UPDATE ... [WHERE]]
[RETURNING expr [AS alias][, ...] [FORMAT type]]
```

Insert one or more rows into the table.

The Insert operation is distributed and will transactionally update table partitions on one or more nodes.
Insert can be part of a multi-statement transaction.

If the table schema is not defined, the table name will be searched in the **`public`** schema.

If the column list is not defined, all values must correspond to the table column types. If the column list is
defined, only the list-defined columns will be set to the corresponding values. Non-defined column values will be
set to **`NULL`**, **`SERIAL`** value or **`DEFAULT`** constraint value will be used (if defined).
If more than one **`SERIAL`** columns are used, they will share the same value.

If the row already exists (according to the primary key), the table primary index unique constraint violation error
will be emitted. The **`ON CONFLICT`** clause allows to change this behavior:

* **`ON CONFLICT DO NOTHING`**

  If the key already exists, ignore the operation.

* **`ON CONFLICT DO ERROR`**

  If the key already exists, throw an error (default INSERT behaviour).

* **`ON CONFLICT DO RESOLVE`**

  If the table has resolved columns, the **`INSERT`** operation will be automatically rewritten as
  update **`INSERT ON CONFLICT DO UPDATE`** using the resolved expressions as
  the update expressions.
  
  If the table has no resolved columns, this operation will be equal
  to **`ON CONFLICT DO ERROR`**.

* **`ON CONFLICT DO UPDATE`**

  If the key already exists, apply the [UPDATE](/docs/sql/dml/update) statement on the existing key.
  The **`excluded.<column>`** prefix can be used to access the inserted row columns.
  Additionally, the **`WHERE`** clause can be used to filter rows.

The **`RETURNING`** clause allows the values to be returned in case of successful completion. The values can
be used as a result in the corresponding [CTE](/docs/sql/transactions/cte) or as a standalone result.

The [FORMAT](/docs/sql/query/format) clause can be used to specify the format of the result.

### Data Ingestion and Streaming

An alternative way to insert different formats directly into a table without using **`SQL`** is to use the
[HTTP API](/docs/api/overview).

---

```SQL
create table example (id int primary key, matches int);
insert into example values (1, 0) on conflict do update set matches = matches + 1;
insert into example values (1, 0) on conflict do update set matches = matches + 1;
insert into example values (1, 0) on conflict do update set matches = matches + 1;
select * from example;
[[1, 2]]
```

```SQL
create table example (device int primary key, metrics json);
insert into example values (48, [1,2,3]), (56, [3,1]);
select * from example;
[[48, [1, 2, 3]], [56, [3, 1]]]
```

```SQL
create table example (id int primary key serial, obj json);

insert into example (obj) values ({"metrics": [1,2,3]});
insert into example (obj) values ({"metrics": [1,2,3]});

select * from example;
[[0, {
  "metrics": [1, 2, 3]
}], [1, {
  "metrics": [1, 2, 3]
}]]
```

```SQL
create table example (
  device_id int primary key,
  hits      int default 1 as ( hits + 1 ) resolved
) with (type = 'hash');

insert into example (device_id) values (1);
insert into example (device_id) values (1) on conflict do resolve;
insert into example (device_id) values (1) on conflict do resolve;

-- ON CONFLICT DO RESOLVE can be ommited, if the table
-- has resolved columns
insert into example (device_id) values (1);

select * from example;
[1, 4]
```

```SQL
-- with CTE
with inserted_items as (
    insert into example values (1), (2), (3) returning *
) select count(*) from inserted_items;
[3]
```
