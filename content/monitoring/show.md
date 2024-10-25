---
weight: 2
title: "SHOW STATUS"
bookToc: false
---

## SHOW STATUS Statement

```SQL
SHOW STATUS
```

Show the essential database and process information gathered in one place.

See also [amelie top](/docs/tutorial/monitoring) command.

---

```SQL
show status
[{
  "uuid": "ad41adcf-6479-f931-a491-2e27272c8a50",
  "version": "1.0.0",
  "frontends": 5,
  "backends": 11,
  "db": {
    "schemas": 2,
    "tables": 0,
    "tables_shared": 0,
    "secondary_indexes": 0,
    "views": 0
  },
  "process": {
    "uptime": 0,
    "mem_virt": 1371725824,
    "mem_resident": 10760192,
    "mem_shared": 5083136,
    "cpu_count": 16,
    "cpu": 26477970,
    "cpu_frontends": [0, 0, 0, 0, 0],
    "cpu_backends": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
  },
  "net": {
    "connections": 1,
    "sent_bytes": 0,
    "recv_bytes": 76
  },
  "wal": {
    "active": true,
    "checkpoint": 15627754,
    "lsn": 15627754,
    "lsn_min": 15593964,
    "files": 1,
    "slots": 0,
    "slots_min": -1,
    "writes": 0,
    "writes_bytes": 0,
    "ops": 0
  },
  "repl": {
    "active": false,
    "role": "primary",
    "primary": null,
    "replicas": {}
  }
}]

select system.status().uuid
["ad41adcf-6479-f931-a491-2e27272c8a50"]
```
