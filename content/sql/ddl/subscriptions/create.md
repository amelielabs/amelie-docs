---
weight: 1
title: "CREATE SUBSCRIPTION"
bookToc: true
---

# CREATE SUBSCRIPTION

```SQL
CREATE SUBSCRIPTION [IF NOT EXISTS] name ON [user.]relation
[DESCRIPTION text]
```

Create a new subscription if it does not exists.

The current user or agent becomes the owner of the subscription.

Subscription holds a persistent state based on the WAL (**LSN**) position, making
sure that all corresponding records after that position (**acknowledged position**)
are still present.

Subscriptions control the behavior of the Change Data Capture (CDC) in the system.
The database maintains an internal in-memory CDC queue for faster read access without IO.

The [ACKNOWLEDGE](/docs/sql/ops/acknowledge) command can be used to advance the position forward.

Please note that the **ACKNOWLEDGE** does WAL write and should be used
with batch processing in mind.

Subscription can be used with [SELECT](/docs/sql/ops/query/select) or as a starting
position for [Real-Time Streaming](/docs/api/http).

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

```SQL
CREATE TABLE example (id int primary key, data int);
CREATE SUBSCRIPTION example_sub ON example;

INSERT INTO example VALUES (1,0), (2,0), (3,0);
DELETE FROM example WHERE id = 2;
UPDATE example SET data = data + 1;

SELECT * FROM example_sub;

lsn  lsn_op  cmd     row
───────────────────────────────────────────
75   0       write   {"id": 1, "data": 0}
75   1       write   {"id": 2, "data": 0}
75   2       write   {"id": 3, "data": 0}
76   0       delete  {"id": 2, "data": 0}
77   0       write   {"id": 3, "data": 1}
77   1       write   {"id": 1, "data": 1}

ACKNOWLEDGE example_sub TO 77, 1;

INSERT INTO example VALUES (4, 0);
SELECT * FROM example_sub;

lsn  lsn_op  cmd    row
──────────────────────────────────────────
80   0       write  {"id": 4, "data": 0}

ACKNOWLEDGE example_sub TO 80;

SELECT count(*) FROM example_sub;

count
─────
0
```
