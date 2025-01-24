---
weight: 1
title: "Overview"
bookToc: false
---

## Reliability

Amelie supports ACID transactions and Commits only if data is written to WAL first (unless it is configured not to do so).

The persistency model is based on classic In-Memory database logic using WAL and monotonically increasing
Log Sequence Number (**`LSN`**) with periodic Snapshotting.

During restart, Amelie finds and reads the latest checkpoint directory and replays WAL changes that happen afterward.
The checkpoint directory keeps snapshot files for each partition separately. All partitions snapshot files are replayed in parallel
for each node individually, reducing start time.

The [CHECKPOINT](/docs/reliability/checkpoint) operation creates snapshots. It is possible to scale this process by creating
and using several workers.  It can be run manually or automatically using periodic intervals. The checkpoint operation is
also responsible for WAL retention and the automatic removal of older checkpoint directories.

---
