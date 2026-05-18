---
weight: 3
title: "ALTER USER"
bookToc: true
---

# ALTER USER Statement

```SQL
ALTER USER|AGENT [IF EXISTS] name RENAME TO name
ALTER USER|AGENT [IF EXISTS] name REVOKE TOKEN
```

Change a user or agent settings if it exists.

The **`REVOKE TOKEN`** command can be used to invalidate all existing
tokens up to this time for the user or agent.

---

```SQL
CREATE AGENT test;
ALTER AGENT test REVOKE TOKEN;

SELECT * FROM SHOW USER test VERBOSE;

user
────
{
  "name": "test",
  "parent": "amelie",
  "created_at": "2026-04-18 14:01:28.789517+03",
  "revoked_at": "2026-05-18 14:01:34.577571+03",
  "agent": true,
  "superuser": false,
  "grants": [["self", "grant", "create_token", "create_table", "create_function", "create_topic", "create_subscription", "rpc", "sql"]]
}
```
