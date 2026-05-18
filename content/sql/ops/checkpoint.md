---
weight: 6
title: "CHECKPOINT"
bookToc: true
---

# CHECKPOINT Statement

```SQL
CHECKPOINT
```

Update catalog file and create new snapshot files for all newly updated partitions.

The checkpoint operation is also responsible for WAL retention.

Normally checkpoint will be automatically scheduled after
reaching the **[wal_checkpoint](/docs/db/admin/configuration)** number of WAL files.

---

```SQL
CHECKPOINT;
```
