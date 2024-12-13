---
weight: 7
title: "SUBSCRIBE"
bookToc: false
---

## SUBSCRIBE Statement

```SQL
SUBSCRIBE id
```

Switch the server to replica by assigning (subscribing) it to the primary server instance **`ID`**.
Replica will accept the primary server which matches this **`ID`**.

After being subscribed, the replica server becomes read-only and will process write
commands only from the primary server.

---

```SQL
-- set primary id on replica server and start the replication
subscribe "00000000-0000-0000-0000-000000000000";
start repl;

show repl;
[{
  "active": true,
  "role": "replica",
  "primary": "00000000-0000-0000-0000-000000000000"
}]

show read_only;
[true]
```
