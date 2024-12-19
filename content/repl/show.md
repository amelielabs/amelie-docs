---
weight: 9
title: "SHOW REPL"
bookToc: false
---

## SHOW REPL Statement

```SQL
SHOW REPLICATION [FORMAT type]
SHOW REPL [FORMAT type]
```

Get the replication status.

The [FORMAT](/docs/sql/query/format) clause can be used to specify the format of the result.

---

```SQL
show repl;
[{
  "active": true,
  "role": "replica",
  "primary": "00000000-0000-0000-0000-000000000000"
}]

select system.repl().active;
[true]
```
