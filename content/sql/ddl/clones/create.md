---
weight: 1
title: "CREATE CLONE"
bookToc: true
---

# CREATE CLONE

```SQL
CREATE CLONE [IF NOT EXISTS] name ON relation
```

Create a new table clone if it does not exists.

The current user or agent becomes the owner of the clone.

Cloness can be used for Git-style temporary workloads or to organize multi-tenancy storage,
where each user or agent will use a dedicated clone instead of a new table.

Table clones are created instantly and operate on the storage level, sharing the same partitions and indexes.
Table indexes will automatically filter rows based on the used clone.

Table clones can be based on table owned by the same or other user or agent. Clones are accessible as
dedicated relations with grants. All DML operations similar to the table are
supported, except **TRUNCATE**.

---

```SQL
CREATE TABLE docs (id int primary key, data int);
INSERT INTO docs VALUES (0, 0), (1, 0), (2, 0);

CREATE CLONE docs_clone OF docs;

SELECT * FROM docs_clone;

id  data
──────────
0   0
1   0
2   0

UPDATE docs_clone SET data = id RETURNING *;

id  data
──────────
0   0
1   1
2   2

SELECT * FROM docs;

id  data
──────────
0   0
1   0
2   0
```
