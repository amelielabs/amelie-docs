---
weight: 1
title: "CREATE USER / AGENT"
bookToc: true
---

# CREATE USER/AGENT Statement

```SQL
CREATE USER|AGENT [IF NOT EXISTS] name
```

Create a user or agent identified by **`name`** if it does not exist.

In Amelie, every user or agent is itself a complete database.  This model eliminates the need for
complex multi-tenancy logic — each user/agent gets its own fully isolated
relational database by default.

---

```SQL
CREATE USER test;

SHOW USERS VERBOSE;

users
─────
{
  "name": "amelie",
  "parent": "amelie",
  "created_at": "2026-05-18 13:27:18.324402+03",
  "revoked_at": "",
  "agent": false,
  "superuser": true,
  "grants": []
}
{
  "name": "test",
  "parent": "amelie",
  "created_at": "2026-05-18 13:54:45.009308+03",
  "revoked_at": "",
  "agent": false,
  "superuser": false,
  "grants": [["self", "grant", "create_token", "create_table", "create_function", "create_topic", "create_subscription", "rpc", "sql"]]
}


```
