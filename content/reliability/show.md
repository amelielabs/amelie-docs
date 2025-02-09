---
weight: 3
title: "SHOW WAL"
bookToc: false
---

## SHOW WAL Statement

```SQL
SHOW WAL [FORMAT type]
```

Get current Write-Ahead Log (WAL) status.

The [FORMAT](/docs/sql/query/format) clause can be used to specify the format of the result.

---

```SQL
show wal;
[{
  "lsn": 1,
  "lsn_min": 1,
  "files": 1,
  "slots": 0,
  "slots_min": -1,
  "writes": 0,
  "writes_bytes": 0,
  "ops": 0,
  "checkpoint": 1
}]
]

select system.wal().files;
[1]
```
