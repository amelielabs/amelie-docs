---
weight: 2
title: "SHOW METRICS"
bookToc: false
---

## SHOW METRICS Statement

```SQL
SHOW METRICS [FORMAT type]
```

Show the essential database and process information gathered in one place.

The [FORMAT](/docs/sql/query/format) clause can be used to specify the format of the result.

See also [amelie top](/docs/tutorial/monitoring) command.

---

```SQL
show metrics;
[{
  "uuid": "cd580566-6cf7-fb90-737d-50dd8abdbc79",
  "version": "0.1.0",
  "frontends": 8,
  "backends": 8,
  "db": {
    "schemas": 2,
    "tables": 1,
    "secondary_indexes": 0
  },
  "process": {
    "uptime": 0,
    "mem_virt": 1371512832,
    "mem_resident": 11137024,
    "mem_shared": 5394432,
    "cpu_count": 16,
    "cpu": 43300122,
    "cpu_frontends": [0, 0, 0, 0, 0, 0, 0, 0],
    "cpu_backends": [0, 0, 0, 0, 0, 0, 0, 0]
  },
  "net": {
    "connections": 1,
    "sent_bytes": 10492,
    "recv_bytes": 1866
  },
  "wal": {
    "lsn": 2,
    "lsn_min": 1,
    "files": 1,
    "slots": 0,
    "slots_min": -1,
    "writes": 1,
    "writes_bytes": 817,
    "ops": 1,
    "checkpoint": 2
  },
  "repl": {
    "active": false,
    "role": "primary",
    "primary": null,
    "replicas": []
  }
}]

select system.metrics().db.tables
[1]
```
