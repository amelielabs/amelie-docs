---
weight: 17
title: '*'
type: docs
bookToc: true
---

## SELECT [target.]*

Stars are used as a placeholder for all target columns in the **`SELECT`** statement.

---

```SQL
CREATE TABLE example (id int primary key);
INSERT INTO example VALUES (1), (2), (3);
SELECT *, test.* FROM test ORDER BY id;

id  id
────────
1   1
2   2
3   3
```
