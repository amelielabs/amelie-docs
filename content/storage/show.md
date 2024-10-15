---
weight: 3
title: "SHOW WAL"
bookToc: false
---

## SHOW WAL Statement

```SQL
SHOW WAL
```

Get current Write-Ahead Log (WAL) status.

---

```SQL
show wal
[{
  "active": true,
  "rotate_wm": 104857600,
  "sync_on_rotate": true,
  "sync_on_write": false,
  "lsn": 210,
  "lsn_min": 1,
  "files": 1,
  "slots": 0,
  "slots_min": -1
}]

select system.wal().files
[1]
```
