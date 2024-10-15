---
weight: 2
title: "CHECKPOINT"
bookToc: false
---

## CHECKPOINT Statement

```SQL
CHECKPOINT [WORKERS n]
```

Create a new database checkpoint.

The new checkpoint will be created in the new directory (inside the base directory) identified by
the current **`LSN`** number. A snapshot file will be created for each table partition in the system.

If the checkpoint identified by the current **`LSN`** already exists, the command
will return without error.

It is possible to scale this process by using several workers. By default, the number of workers
is set as defined in the **`checkpoint_workers`** config variable. The **`checkpoint_interval`** variable can be
configured to run the checkpoint operation periodically. It is set to 5 minutes by default.

The checkpoint operation is also responsible for WAL retention and automatically removing older
checkpoint directories.

---

```SQL
checkpoint

show checkpoint_interval
["5 min"]

show checkpoint_workers
[3]

show checkpoint
[210]

show lsn
[210]
```
