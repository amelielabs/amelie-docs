---
weight: 1
title: "ALTER SYSTEM"
bookToc: true
---

# ALTER SYSTEM

```SQL
ALTER SYSTEM SECRET ROTATE
```

Change system-wide settings.

### SECRET ROTATE 

The server is using an internal, randomly generated secret to sign and
validate server-issued tokens. The secret is not exposed outside.

This command generates a new secret and invalidates all previously issued tokens.

It is also possible to [REVOKE TOKEN](/docs/sql/ddl/users/alter) per user or agent.

---

```SQL
ALTER SYSTEM SECRET ROTATE;
```
