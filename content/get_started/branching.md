---
weight: 3
title: Branching
bookToc: true
---

# Table Branching

One of Amelie’s most powerful features is **instant branching** — you can create a complete,
writable branch of any table (or even another branch) in milliseconds.

[Branches](/docs/sql/ddl/branches/create) work at the storage level, sharing the same underlying partitions and indexes while maintaining
full isolation. Indexes automatically filter rows based on the active branch.
Each branch is accessible as its own dedicated relation, with independent grants and permissions.

```SQL
CREATE BRANCH documents_branch FROM documents;
```

### Use Cases

* **Git-style workflows** for safe experimentation and versioning
* **Multi-tenancy at scale** — thousands of users or agents can safely share the same tables and indexes
while maintaining strong isolation and independent access control

Branches give you the flexibility of separate databases with the efficiency of shared storage.
