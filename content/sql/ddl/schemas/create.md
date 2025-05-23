---
weight: 1
title: "CREATE SCHEMA"
bookToc: false
---

## CREATE SCHEMA Statement

```SQL
CREATE SCHEMA [IF NOT EXISTS] name
```

Create a new schema object unless it already exists.

Schemas allow for the logical grouping of objects such as tables, and functions into namespaces.
Currently, the **`CREATE SCHEMA`** operation cannot be part of multi-statement transactions.

Amelie has two predefined system schemas: **`system`** and **`public`**.

---

```SQL
create schema example;

show schemas;
[{"name": "system"}, {"name": "public"}, {"name": "example"}]
```
