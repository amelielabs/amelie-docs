---
weight: 1
title: "CREATE TOPIC"
bookToc: true
---

# CREATE TOPIC

```SQL
CREATE TOPIC [IF NOT EXISTS] name
[DESCRIPTION text]
```

Create a new topic if it does not exists.

The current user or agent becomes the owner of the topic.

Topics implement Pub/Sub queues. Unlike tables, topics do not have a schema
(everything is converted to JSON) and do not store data like tables do.

Instead, [PUBLISH](/docs/sql/ops/dml/publish) command writes directly to the in-memory CDC queue and the WAL, which
allows the creation of a real-time communication layer for subscribers.

If topic has no [SUBSCRIPTIONS](/docs/sql/ddl/subscriptions/create), the **PUBLISH** command will do nothing.

Topics are transactional and can be used in multi-statement transactions.

---

```SQL
CREATE TOPIC channel;
CREATE SUBSCRIPTION channel_sub ON channel;
PUBLISH INTO channel "Hello World!";
PUBLISH INTO channel 1, 2, 3;

SELECT * FROM channel_sub;

lsn  lsn_op  cmd      row
──────────────────────────────────────
70   0       publish  "Hello World!"
71   0       publish  1
71   1       publish  2
71   2       publish  3
```
