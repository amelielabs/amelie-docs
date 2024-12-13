---
title: Introduction
type: docs
bookToc: false
---

![image description](/docs/logo.png)

## Introduction

Amelie is a lightweight OLTP SQL relational database that focuses on performance and throughput for
short ACID transactions and real-time analytics. Its unique architecture is designed for full
parallelization and lockless transaction execution.

Amelie works over HTTP and does not require additional client libraries. Any modern programming
language or tooling that supports HTTP and JSON can be used directly.

Learn more about its [Architecture](/docs/architecture/) and [Get Started](/docs/tutorial/get_started).

---

#### SQL Reference

<span style="background: gray; font-size: 13px; font-family: IBM Plex Mono, monospace;">

{{% columns %}}

* [CREATE SCHEMA](/docs/sql/ddl/schemas/create)
* [CREATE TABLE](/docs/sql/ddl/tables/create)
* [CREATE INDEX](/docs/sql/ddl/indexes/create)
* [CREATE USER](/docs/users/create)
* [CREATE NODE](/docs/cluster/create)
* [CREATE REPLICA](/docs/repl/create)
* [CREATE TOKEN](/docs/users/create_token)

<--->

* [DROP SCHEMA](/docs/sql/ddl/schemas/drop)
* [DROP TABLE](/docs/sql/ddl/tables/drop)
* [DROP INDEX](/docs/sql/ddl/indexes/drop)
* [DROP USER](/docs/users/drop)
* [DROP NODE](/docs/cluster/drop)
* [DROP REPLICA](/docs/repl/drop)

<--->

* [ALTER SCHEMA](/docs/sql/ddl/schemas/alter)
* [ALTER TABLE](/docs/sql/ddl/tables/alter)
* [ALTER INDEX](/docs/sql/ddl/indexes/alter)

{{% /columns %}}


{{% columns %}}

* [INSERT / UPSERT](/docs/sql/dml/insert)
* [UPDATE](/docs/sql/dml/update)
* [DELETE](/docs/sql/dml/delete)
* [TRUNCATE](/docs/sql/dml/truncate)

<--->

* [SELECT](/docs/sql/query/select)

<--->

* [Functions](/docs/sql/functions/system)
* [Expressions](/docs/sql/expressions/arithmetical)
* [Aggregates](/docs/sql/query/aggregates)
* [Lambda](/docs/sql/query/lambda)

{{% /columns %}}


{{% columns %}}

* [START REPLICATION](/docs/repl/start)
* [SUBSCRIBE](/docs/repl/subscribe)
* [CHECKPOINT](/docs/storage/checkpoint)

<--->

* [STOP REPLICATION](/docs/repl/stop)
* [UNSUBSCRIBE](/docs/repl/unsubscribe)

<--->

{{% /columns %}}


{{% columns %}}

* [SHOW SCHEMAS](/docs/sql/ddl/schemas/show)
* [SHOW TABLES](/docs/sql/ddl/tables/show)

<--->

* [SHOW USERS](/docs/users/show)
* [SHOW NODES](/docs/cluster/show)
* [SHOW REPLICAS](/docs/repl/show_replicas)
* [SHOW REPLICATION](/docs/repl/show)
* [SHOW WAL](/docs/storage/show)

<--->

* [SHOW ALL](/docs/configuration/show)
* [SHOW CONFIG](/docs/configuration/show)
* [SET](/docs/configuration/set)

{{% /columns %}}

</span>

---
