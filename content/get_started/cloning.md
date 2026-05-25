---
weight: 3
title: Table Cloning
bookToc: true
---

# Table Cloning

One of Amelie’s most powerful features is **instant cloning** — you can create a complete,
writable clone of any table in milliseconds.

Table [Clones](/docs/sql/ddl/clones/create) work at the storage level, sharing the same underlying partitions and indexes while maintaining
full isolation. Indexes automatically filter rows based on the active clone.
Each table clone is accessible as its own dedicated relation, with independent grants and permissions.

```SQL
CREATE CLONE docs OF some_user.docs;
```

### Use Cases

* **Git-style workflows** for safe experimentation and versioning
* **Multi-tenancy at scale** — thousands of users or agents can safely share the same tables, partitions, and
  indexes while maintaining strong isolation and independent access control

Clones give you the flexibility of separate tables with the efficiency of shared storage.
