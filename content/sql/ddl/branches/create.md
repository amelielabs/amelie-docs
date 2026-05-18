---
weight: 1
title: "CREATE BRANCH"
bookToc: true
---

# CREATE BRANCH Statement

```SQL
CREATE BRANCH [IF NOT EXISTS] name FROM relation
```

Create a new branch if it does not exists.

The current user or agent becomes the owner of the branch.

Branches can be used for Git-style temporary workloads or to organize multi-tenancy storage,
where each user or agent will use a branch instead of a new table.

Branches are created instantly and operate on the storage level, sharing the same indexes. Table indexes will
automatically filter rows based on the used branch.

Table branches can be based on tables or other branches. Branches are accessible as
dedicated relations with grants. All DML operations similar to the table are
supported, except **TRUNCATE**.

---

```SQL
CREATE TABLE example (id int primary key, data int);
INSERT INTO example VALUES (0, 0), (1, 0), (2, 0);

CREATE BRANCH A FROM example;
SELECT * FROM A;

id  data
──────────
0   0
1   0
2   0

UPDATE A SET data = id;

id  data
──────────
0   0
1   1
2   2

SELECT * FROM example;
...
```
