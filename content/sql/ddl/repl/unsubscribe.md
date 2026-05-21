---
weight: 8
title: "UNSUBSCRIBE"
bookToc: true
---

# UNSUBSCRIBE

```SQL
UNSUBSCRIBE
```

Unsubscribe from the primary server and become the primary server itself.

---

```SQL
UNSUBSCRIBE;

repl
────
{
  "active": false,
  "role": "primary",
  "primary": null,
  "replicas": []
}
```
