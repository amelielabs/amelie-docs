---
weight: 8
title: Monitoring
bookToc: true
---

# Monitoring

The [SHOW](/docs/sql/ops/show) command can be used to get information about the system state.

All system information stored and presented in JSON.

---

```sql
SHOW TABLES;

tables
──────
{
  "user": "amelie",
  "name": "test"
}

SELECT * FROM SHOW TABLES;

tables
──────
{
  "user": "amelie",
  "name": "test"
}
```
