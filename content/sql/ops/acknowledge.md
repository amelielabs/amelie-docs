---
weight: 6
title: "ACKNOWLEDGE"
bookToc: true
---

# ACKNOWLEDGE

```SQL
ACKNOWLEDGE subscription TO lsn[, lsn_op]
```

Subscription holds a persistent state based on the WAL (**LSN**) position, making
sure that all corresponding records after that position (**acknowledged position**)
are still present.

The **ACKNOWLEDGE** command is used to advance the subscription position forward.

Please note that the **ACKNOWLEDGE** does WAL write and should be used
with batch processing in mind.

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

ACKNOWLEDGE channel_sub TO 71, 2;
```
