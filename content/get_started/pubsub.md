---
weight: 4
title: Pub/Sub
bookToc: true
---

# Pub/Sub

Amelie provides a powerful, built-in **Pub/Sub** system through the concept of **Topics**.

Unlike regular tables, topics are lightweight and schemaless — every message is automatically converted to JSON.
When you publish to a topic, the message is written to the WAL and immediately distributed in real-time
to all active subscribers through the in-memory CDC queue.

Designed to work together with [Change Data Capture](/docs/get_started/cdc) and [Real-Time Streaming](/docs/get_started/streaming).

```SQL
CREATE TOPIC user_events;
CREATE SUBSCRIPTION user_events_sub ON user_events;

PUBLISH INTO user_events
{
 "type": "user_logged_in",
 "user_id": 42
};
```

### Key Benefits

* **Real-time messaging** — Messages are delivered instantly to subscribers
* **Transactional** — [PUBLISH](/docs/sql/ops/dml/publish/) respects transaction boundaries
* **Unlogged topics** — Create [UNLOGGED TOPIC](/docs/sql/ddl/topics/create) for maximum speed when durability isn’t needed
* **Simple & scalable** — Perfect for coordination, live updates, and event-driven architectures

Topics give you Kafka-style event streaming with the simplicity and integration of a relational database.
