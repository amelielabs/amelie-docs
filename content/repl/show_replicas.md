---
weight: 4
title: "SHOW REPLICAS"
bookToc: false
---

## SHOW REPLICAS Statement

Get a list of the status of replica servers.

---

```SQL
show replicas;
[{
  "00000000-0000-0000-0000-000000000001": {
    "id": "00000000-0000-0000-0000-000000000001",
    "uri": "http://localhost:3481",
    "connected": false,
    "lsn": 0,
    "lag": 210
  }
}]

select system.replicas()['00000000-0000-0000-0000-000000000001'];
[{
  "id": "00000000-0000-0000-0000-000000000001",
  "uri": "http://localhost:3481",
  "connected": false,
  "lsn": 0,
  "lag": 210
}]
```
