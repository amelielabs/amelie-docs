---
weight: 5
title: TRUNCATE
type: docs
bookToc: false
---

## TRUNCATE Statement

```SQL
TRUNCATE [schema.]table_name
```

Empty rows in the table.

If the table schema is not defined, the table name will be searched in the **`public`** schema.

Currently, the **`TRUNCATE`** operation cannot be part of multi-statement transactions.
it is recommended to run the [CHECKPOINT](/docs/storage/checkpoint) operation right after its completion.

---

```SQL
create table test (id int primary key)

insert into test values (1)
insert into test values (2)
insert into test values (2)

truncate test

select * from test
[]
```
