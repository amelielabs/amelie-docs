---
weight: 4
title: "SHOW REPLICA"
bookToc: false
---

## SHOW REPLICA Statement

```SQL
SHOW REPLICAS [FORMAT type]
SHOW REPLICA name [FORMAT type]
```

Get a list of the status of replica servers.

---

```SQL
show replicas;
[{
  "id": "00000000-0000-0000-0000-000000000001",
  "uri": "http://localhost:3481",
  "connected": false,
  "lsn": 0,
  "lag": 7
}]

select id from system.replicas();
["00000000-0000-0000-0000-000000000001"]

show replica '00000000-0000-0000-0000-000000000001';
[{
  "id": "00000000-0000-0000-0000-000000000001",
  "uri": "http://localhost:3481",
  "connected": false,
  "lsn": 0,
  "lag": 7
}]

select system.replica('00000000-0000-0000-0000-000000000001').uri;
["http://localhost:3481"]
```
