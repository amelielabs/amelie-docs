---
title: Introduction
type: docs
bookToc: false
---

![image description](/docs/logo.png)

### Introduction

Amelie is a lightweight, full-featured, in-memory OLTP SQL relational database that
allows full parallelization and lockless transaction processing.
It scales linearly with the number of CPU cores both for IO and Compute separately,
performs automatic partitioning, and generates parallel group plans for
all types of queries.

Amelie has support for [Hot Backup](/docs/tutorial/backup) and [Async Logical Replication](/docs/repl/overview), which allows
fault-tolerant primary-replica setups to be created.

The [SQL](/docs/sql/overview) commands can be executed, or data can be imported using the [HTTP API](/docs/api/execute) or [CLI](/docs/tutorial/cli).

Learn more about [How It Works](/docs/compute/overview) and [Get Started](/docs/tutorial/get_started).

---

### Quick Reference

<span style="background: gray; font-size: 13px; font-family: IBM Plex Mono, monospace;">

{{% columns %}}

#### DDL

* [CREATE SCHEMA](/docs/sql/ddl/schemas/create)
* [CREATE TABLE](/docs/sql/ddl/tables/create)
* [CREATE INDEX](/docs/sql/ddl/indexes/create)
* [CREATE USER](/docs/users/create)
* [CREATE REPLICA](/docs/repl/create)
* [CREATE BACKEND](/docs/compute/create)
* [CREATE TOKEN](/docs/users/create_token)

<--->

#### &nbsp;

* [DROP SCHEMA](/docs/sql/ddl/schemas/drop)
* [DROP TABLE](/docs/sql/ddl/tables/drop)
* [DROP INDEX](/docs/sql/ddl/indexes/drop)
* [DROP USER](/docs/users/drop)
* [DROP REPLICA](/docs/repl/drop)
* [DROP BACKEND](/docs/compute/drop)

<--->

#### &nbsp;

* [ALTER SCHEMA](/docs/sql/ddl/schemas/alter)
* [ALTER TABLE](/docs/sql/ddl/tables/alter)
* [ALTER INDEX](/docs/sql/ddl/indexes/alter)

{{% /columns %}}


{{% columns %}}

#### DML


* [INSERT / UPSERT](/docs/sql/dml/insert)
* [UPDATE](/docs/sql/dml/update)
* [DELETE](/docs/sql/dml/delete)
* [TRUNCATE](/docs/sql/dml/truncate)

<--->

#### Query

* [SELECT](/docs/sql/query/select)

<--->

#### &nbsp;

* [Types](/docs/sql/types/bool)
* [Functions](/docs/sql/functions/casting)
* [Expressions](/docs/sql/expressions/arithmetical)
* [Aggregates](/docs/sql/query/aggregates)
* [Lambda](/docs/sql/query/lambda)

{{% /columns %}}

{{% columns %}}

#### Transactions

* [BEGIN / COMMIT](/docs/sql/begin_commit)
* [CTE](/docs/sql/cte)

<--->

#### &nbsp;

* [EXPLAIN](/docs/sql/explain)

<--->

{{% /columns %}}


{{% columns %}}

#### Replication

* [START REPLICATION](/docs/repl/start)
* [SUBSCRIBE](/docs/repl/subscribe)
* [CHECKPOINT](/docs/reliability/checkpoint)

<--->

#### &nbsp;

* [STOP REPLICATION](/docs/repl/stop)
* [UNSUBSCRIBE](/docs/repl/unsubscribe)

<--->

{{% /columns %}}


{{% columns %}}

#### System

* [SHOW SCHEMAS](/docs/sql/ddl/schemas/show)
* [SHOW SCHEMA](/docs/sql/ddl/schemas/show)
* [SHOW TABLES](/docs/sql/ddl/tables/show)
* [SHOW TABLE](/docs/sql/ddl/tables/show)

<--->

#### &nbsp;

* [SHOW USERS](/docs/users/show)
* [SHOW USER](/docs/users/show)
* [SHOW BACKENDS](/docs/compute/show)
* [SHOW REPLICAS](/docs/repl/show_replica)
* [SHOW REPLICA](/docs/repl/show_replica)
* [SHOW REPLICATION](/docs/repl/show)
* [SHOW WAL](/docs/reliability/show)
* [SHOW METRICS](/docs/monitoring/show)
* [SHOW STATE](/docs/monitoring/show_state)

<--->

#### &nbsp;

* [SHOW CONFIG](/docs/configuration/show)
* [SET](/docs/configuration/set)

{{% /columns %}}

</span>

---
