---
weight: 9
title: "Cluster"
bookToc: false
---

## Cluster Settings

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----:       | :---- |
| frontends         |  int     | cli          | Number of frontend workers |
| backends          |  int     | init cli     | Number of backend workers (compute nodes) |

---

```SQL
show frontends
[5]

show backends
[12]
```
