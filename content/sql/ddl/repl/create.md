---
weight: 2
title: "CREATE REPLICA"
bookToc: true
---

# CREATE REPLICA

```SQL
CREATE REPLICA [IF NOT EXISTS] ID URI
```

Define a new replica by UUID unless it exists. The replica ID must match the replica server instance ID.

Replica connection will start automatically if the replication is active.

---

```SQL
-- switch to replica
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

```SQL
-- create new replica on the primary server and start replication
CREATE REPLICA "00000000-0000-0000-0000-000000000001" "127.0.0.1:3481";

SHOW REPL;

repl
────
{
  "active": false,
  "role": "primary",
  "primary": null,
  "replicas": [{
    "id": "00000000-0000-0000-0000-000000000001",
    "uri": "http://127.0.0.1:3481/",
    "connected": false,
    "lsn": 0,
    "lag": 12
  }]
}

START REPL;
```
