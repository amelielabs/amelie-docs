---
weight: 1
title: "CREATE STORAGE"
bookToc: true
---

# CREATE STORAGE Statement

```SQL
CREATE STORAGE [IF NOT EXISTS] name [(options)]
```

Create a new storage if it does not exists.

Storages are system-wide objects designed to work together with tables.

Storages allows the creation and definition of additional secondary repositories
to extend disk storage capacity and increase IOPS without downtime.

Follow options are supported:

| Name              | Description |
| :---------------- | :---- |
| path              | directory path (if not defined, will use repository) |
| compression       | compression type (set to **zstd** by default) |
| compression_level | compression level |

**main** storage always exists and point to the repository.

---

```SQL
CREATE STORAGE ssd (path '/mnt/ssd');
CREATE TABLE example (id int primary key) ON STORAGE ssd;

storages
────────
{
  "name": "main",
  "path": "",
  "compression": "zstd",
  "compression_level": 0
}
{
  "name": "ssd",
  "path": "/mnt/ssd",
  "compression": "zstd",
  "compression_level": 0
}
```
