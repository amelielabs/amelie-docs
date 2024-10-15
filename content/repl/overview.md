---
weight: 1
title: "Overview"
bookToc: false
---

## Replication

Amelie supports Asynchronous Replication, which allows fault-tolerant Primary-Replica setups to
be created. Replication is logical and based on WAL streaming. 

Replica servers can be defined on the Primary server using the [CREATE REPLICA](/docs/repl/create) statement. 

The replica server must be created initially from the primary server backup, have a unique instance **`UUID`** and be up-to-date
with Primary WAL. Replica servers must be [SUBSCRIBED](/docs/repl/subscribe) to the Primary ID to accept the
Primary server connection.  The [UNSUBSCRIBE](/docs/repl/unsubscribe) command can be used to unsubscribe from the
primary server and become the primary server itself.

The Primary server connects to replica servers identified by the created replica object and continuously
streams WAL changes.

The replica server can become outdated if its **`WAL LSN`** is no longer available on the Primary server
(because of [CHECKPOINT](/docs/storage/checkpoint) operation). To prevent this, the primary server creates replication
slots to identify replica positions. Replication slots are continuously advanced and synced with replica states.
They are used to keep older WAL files until all replicas are in sync.

[START/STOP REPLICATION](/docs/repl/start) commands can enable or disable replication on a server.
