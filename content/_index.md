---
title: Introduction
type: docs
bookToc: true
---


## Introduction

Amelie is a lightweight, full-featured, in-memory OLTP SQL relational database that
allows full parallelization and lockless transaction processing.

It scales linearly with the number of CPU cores both for IO and Compute separately,
performs automatic partitioning, and generates parallel group plans for
all types of queries.

Fast OLTP, parallel vector search, instant branching, pub/sub,
and real-time event streaming —  all unified in one
in-memory relational database.

Amelie has support for [Hot Backup](/docs/tutorial/backup) and [Async Logical Replication](/docs/repl/overview), which allows
fault-tolerant primary-replica setups to be created.

The [SQL](/docs/sql/overview) commands can be executed, or data can be imported using the [HTTP API](/docs/api/execute) or [CLI](/docs/tutorial/cli).

Learn more about [How It Works](/docs/compute/overview) and [Get Started](/docs/tutorial/get_started).
