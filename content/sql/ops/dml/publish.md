---
weight: 5
title: PUBLISH
type: docs
bookToc: true
---

# PUBLISH

```SQL
PUBLISH TO [user.]topic [value, ...]
```

Publish zero or more values to the topic.

**PUBLISH** command writes directly to the in-memory CDC queue and the WAL, which
allows the creation of a real-time communication layer for subscribers.

Publish can be used for batch publishing more then one value at once.

If topic has no [SUBSCRIPTIONS](/docs/sql/ddl/subscriptions/create), the **PUBLISH** command will do nothing.

---

```SQL
CREATE TOPIC channel;
CREATE SUBSCRIPTION channel_sub ON channel;
PUBLISH TO channel "Hello World!";
PUBLISH TO channel 1, 2, 3;

SELECT * FROM channel_sub;

lsn  lsn_op  cmd      row
──────────────────────────────────────
70   0       publish  "Hello World!"
71   0       publish  1
71   1       publish  2
71   2       publish  3

ACKNOWLEDGE channel_sub TO 71, 2;
```
