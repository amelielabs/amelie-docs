---
weight: 3
title: "ALTER TOPIC"
bookToc: true
---

# ALTER TOPIC

```SQL
ALTER TOPIC [IF EXISTS] name RENAME TO name
```

Change the definition of a topic if it exists.

Currently, the **`ALTER TOPIC`** operation cannot be part of multi-statement transactions.

---

```SQL
ALTER TOPIC channel RENAME TO channel_prev;
```
