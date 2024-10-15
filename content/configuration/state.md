---
weight: 13
title: "State"
bookToc: false
---

## System State

| Name                | Type     | Mode         | Description |
| :----------------   | :------: | :----:       | :---- |
| read_only           | bool     |  read-only   | System in read-only mode cannot accept writes |
| lsn                 | int      |  read-only   | Log Sequence Number |
| psn                 | int      |  read-only   | Partition Sequence Number  |

---

```SQL
show lsn
[56]
```
