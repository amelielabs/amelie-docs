---
weight: 10
title: "WAL"
bookToc: false
---

## WAL Settings

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----:       | :---- |
| wal               |  bool    | cli          | Enable/disable WAL (enabled by default) |
| wal_rotate_wm     |  int     | cli, session | The number of operations per WAL file. When the current WAL file reaches this value, a new file will be created |
| wal_sync_on_rotate |  bool   | cli | Sync the previous WAL file when a new one is created (enabled by default) |
| wal_sync_on_write |  bool    | cli | Sync the current WAL file on each write (disabled by default) |

---

```SQL
select system.config().wal
[true]

show wal
[{
  "active": true,
  "rotate_wm": 104857600,
  "sync_on_rotate": true,
  "sync_on_write": false,
  "lsn": 210,
  "lsn_min": 1,
  "files": 2,
  "slots": 1,
  "slots_min": -1
}]
```
