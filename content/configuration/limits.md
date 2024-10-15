---
weight: 8
title: "Limits"
bookToc: false
---

## Session Limits

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----:       | :---- |
| limit_send        |  int     | cli, session | Limit for reply (bytes) |
| limit_recv        |  int     | cli, session | Limit for request (bytes) |
| limit_write       |  int     | cli, session | Limit for transaction log size (bytes) |

---

```SQL
show limit_send
[3145728]

show limit_recv
[1048576]

show limit_write
[0]
```
