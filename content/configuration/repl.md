---
weight: 11
title: "Replication"
bookToc: false
---

## Replication Settings

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----:       | :---- |
| repl              |  bool    | cli          | Enable/Disable replication (disabled by default) |
| repl_primary      |  string  | cli          | Replication primary server ID |
| repl_reconnect_ms |  int     | cli, session | Reconnect interval in ms |

Variables **`repl`** and **`repl_primary`** are changed automatically by the replication commands.

---

```SQL
show repl_reconnect_ms
[3000]

show repl
[{
  "active": false,
  "role": "primary",
  "primary": null
}]
```
