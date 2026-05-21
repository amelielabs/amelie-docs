---
weight: 7
title: "SUBSCRIBE"
bookToc: true
---

# SUBSCRIBE

```SQL
SUBSCRIBE id
```

Switch the server to replica by assigning (subscribing) it to the primary server instance **`ID`**.
Replica will accept the primary server which matches this **`ID`**.

After being subscribed, the replica server becomes read-only and will process write
commands only from the primary server.

---

```SQL
-- subscribe to the primary (and become replica)
START REPL;
SUBSCRIBE "00000000-0000-0000-0000-000000000000";

SHOW REPL;

repl
────
{
  "active": true,
  "role": "replica",
  "primary": "00000000-0000-0000-0000-000000000000",
  "replicas": []
}
```
