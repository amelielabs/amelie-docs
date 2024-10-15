---
weight: 3
title: UPDATE
type: docs
bookToc: false
---

## UPDATE Statement

```SQL
UPDATE [schema.]table_name SET column[.path] = expr[, ... ]
[WHERE expr]
[RETURNING expr [INTO cte]]
```

Update rows in the table.

The Update operation is distributed and will transactionally update table partitions on one or more nodes.
Update can be part of a multi-statement transaction.

If the table schema is not defined, the table name will be searched in the **`public`** schema.

The path path can be nested if the update column is a **`OBJECT`**.

The **`RETURNING`** clause allows the defined expression value to be returned in case of successful completion. This value can
be used as a result in the corresponding [CTE](/docs/sql/transactions/cte) or as a standalone result.

The **`INTO`** clause provides an alternative way to define this statement as a [CTE](/docs/sql/transactions/cte).

---

```SQL
create table test (id int primary key, data array)
insert into test values (1, [1,2,3]), (2, ['a', 'b', 'c'])

select data from test
[[1, 2, 3], ["a", "b", "c"]]

update test set data = data::append(4) where id = 1 returning *
[[1, [1, 2, 3, 4]]]
```

```SQL
create table test (id int primary key, obj object)
insert into test values (1, {"id": 1, "data": null})

update test set obj.data = [1,2,3] returning *
[[1, {
  "id": 1,
  "data": [1, 2, 3]
}]]

update test set obj.data = obj.data::append(4) returning *
[[1, {
  "id": 1,
  "data": [1, 2, 3, 4]
}]]
```

```SQL
-- with CTE
with updated_items as (
    update test set data = data::append(4) where id = 1 returning *
) select count(*) from updated_items
[1]

-- alternative CTE form using RETURNING INTO
update test set data = data::append(4) where id = 1 returning * into updated_items;
select count(*) from updated_items
[1]

update test set data = data::append(4) where id = 1 returning * into updated_items;
select updated_items::size
[1]
```
