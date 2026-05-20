---
weight: 5
title: Change Data Capture (CDC)
bookToc: true
---

# Change Data Capture (CDC)

Amelie offers powerful, built-in **Change Data Capture (CDC)** system through persistent **Subscriptions**.

You can create a [SUBSCRIPTION](/docs/sql/ddl/subscriptions/create) on any **table** or **topic**:

```sql
CREATE SUBSCRIPTION order_changes ON orders;
```

Each subscription maintains its own position in the WAL (via LSN), allowing you to:

* Query historical changes
* Resume from where you left off
* Power real-time streaming

### How CDC Works in Amelie

* The database maintains a fast in-memory CDC queue for low-latency access
* Changes are written to the WAL for durability
* You can consume changes either through regular [SELECT](/docs/sql/ops/query/select) queries or
through [Real-Time Streaming](/docs/get_started/streaming) via a WebSocket connection.

### Advancing Position

Use the [ACKNOWLEDGE](/docs/sql/ops/acknowledge) command to move the subscription forward:

```sql
ACKNOWLEDGE order_changes TO 42;
```

This makes Subscriptions perfect for both batch processing and real-time event streaming.
