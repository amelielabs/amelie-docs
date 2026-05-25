---
weight: 4
title: "GRANT / REVOKE"
bookToc: true
---

# GRANT / REVOKE

```SQL
GRANT  permission, ... [ON relation] TO user
REVOKE permission, ... [ON relation] FROM user
```

Grant or revoke one or more permissions to or from a user.

Learn more about [Permissions](/docs/sql/ddl/users/permissions).

---

```SQL
GRANT select ON example_table TO someuser;
GRANT create_clone ON example_table TO someuser;

SHOW GRANTS ON example_table;

grants
──────
["someuser", "create_clone", "select"]
```
