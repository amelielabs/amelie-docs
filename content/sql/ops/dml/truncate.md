---
weight: 4
title: TRUNCATE
type: docs
bookToc: true
---

# TRUNCATE

```SQL
TRUNCATE [user.]table_name
```

Empty rows in the table.

If the user is not defined, the table name will be searched for the current user or agent.

Currently, the **`TRUNCATE`** operation cannot be part of multi-statement transactions.

Trancate cannot be used with branches.

---

```SQL
CREATE TABLE example (id int primary key);

INSERT INTO example VALUES (1);
INSERT INTO example VALUES (2);
INSERT INTO example VALUES (2);

TRUNCATE example;

SELECT count(*) FROM example;

count
─────
0
```
