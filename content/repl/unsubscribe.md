---
weight: 8
title: "UNSUBSCRIBE"
bookToc: false
---

## UNSUBSCRIBE Statement

```SQL
UNSUBSCRIBE
```

Unsubscribe from the primary server and become the primary server itself.

---

```SQL
-- set primary id on replica server and start the replication
subscribe "00000000-0000-0000-0000-000000000000";
start repl;

show read_only;
[true]

show repl;
[{
  "active": true,
  "role": "replica",
  "primary": "00000000-0000-0000-0000-000000000000"
}]

unsubscribe;

show read_only;
[false]

show repl;
[{
  "active": true,
  "role": "primary",
  "primary": null
}]
```
