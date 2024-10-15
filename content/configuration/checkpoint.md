---
weight: 12
title: "Checkpoint"
bookToc: false
---

## Checkpoint

| Name                | Type     | Mode         | Description |
| :----------------   | :------: | :----:       | :---- |
| checkpoint_interval | interval | cli          | 5 minutes by default |
| checkpoint_workers  | int      | cli          | Number of workers which will be created during checkpoint (3 by default) |
| checkpoint          | int      | cli          | Last checkpoint LSN |

---

```SQL
show checkpoint
[56]
```
