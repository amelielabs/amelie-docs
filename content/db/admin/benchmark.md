---
weight: 10
title: Benchmarking
bookToc: true
---

# Benchmarking

The **`amelie bench [options]`** command can be used for server benchmarking
using predefined tests. The command is compatible with the [Console Client](/docs/db/admin/cli) options.

The following benchmarking options are supported:

| Argument          | Type | Description |
| :---------------- |  :----:  | :----      |
| type          | string | Benchmark type: **`tpcb`** (default), **`insert`**, **`upsert`**, **`resolved`**, **`decre`**. |
| threads       | int | Number of client threads (default is 1). |
| clients       | int | Total number of clients (default is 32). |
| time          | int | Time in seconds (default is 10). |
| batch         | int | Number of rows in one insert/upsert statement (default is 64). |
| scale         | int | The scale factor for `tpcb` test (default is 1). |
| init          | bool | Prepare tables for testing (default is true). |
| unlogged      | bool | Mark tables as unlogged (default is false). |
| histogram     | bool | Measure times (default is false). |

### Recommendations

Please note that the number of **`frontends`**, **`backends`** in the system, as well as using **`unlogged`** tables directly
impact the performance. It is a good idea to start with minimumal numbers (or defaults) and then alter them
to see how it affects the performance.

More is not always better, especially if you are running benchmarks on the same machine. There is a possible
situation when workers will start competing for CPU cores and locking each other. Likely it would be better to keep total number
of frontends and backends less or equal then the number of available physical CPU cores.

[Learn more](/docs/db/architecture/overview) about the IO and Compute.

### TPC-B Style Benchmark

This is the default benchmarking type, made to match the [PostgreSQL pgbench](https://www.postgresql.org/docs/current/pgbench.html) command to get an exact
performance comparison with PostgreSQL.

It continuously executes the following multi-statement transaction, which involves four tables.

Please note, that the Amelie benchmark will batch transactions to give more preasure on compute (otherwise we are measuring round-trip).

```SQL
BEGIN

UPDATE accounts
   SET abalance = abalance + :delta
 WHERE aid = :aid;

SELECT abalance into :abalance
  FROM accounts
 WHERE aid = :aid;

UPDATE tellers
   SET tbalance = tbalance + :delta
 WHERE tid = :tid;

UPDATE branches
   SET bbalance = bbalance + :delta
 WHERE bid = :bid;

INSERT INTO history (tid, bid, aid, delta, time)
VALUES (:tid, :bid, :aid, :delta, current_timestamp);

END
```

### Debit/Credit Benchmark

Execute basic financial transactions which include two update. The number of transactions per one round-trip can be configured using
the **`batch`** option (try lower values). The test table's primary index is **`hash`**.

### Insert Benchmark

Sequentially Insert rows using the [INSERT](/docs/sql/ops/dml/insert) statement. The number of rows per one operation can be configured using
the **`batch`** option. The test table's primary index is **`tree`**.

Watch out for available RAM.

### Upsert Benchmark

Randomly Insert rows using the [INSERT ON CONFLICT DO UPDATE](/docs/sql/ops/dml/insert) statement. The number of rows per one operation
can be configured using the **`batch`** option. The test table's primary index is **`hash`**.

The number of rows in the table is set to 100000 random keys.

### Resolved Benchmark

Randomly Insert rows where each column is generated as **`stored`** or **`resolved`** together. The number of rows per one operation
can be configured using the **`batch`** option. The test table's primary index is **`hash`**.

```SQL
CREATE TABLE test
(
  ts   timestamp as ( current_timestamp::date_bin('3 sec'::interval) ) stored,
  id   int as identity random (10000),
  hits int default 0 as ( hits + 1 ) resolved,
  primary key(ts, id) using hash
);
```

### Third-Party Benchmarking tools

Using any HTTP benchmarking tool configured to generate custom requests is possible.

Please ensure the benchmarking tool can adequately adjust the pressure level to match the processing capabilities.

One such tool is [wrk](https://github.com/wg/wrk/tree/master).

---

```sh
# do tpcb style benchmark for 1 minute
amelie bench http://localhost --time=60

# do batch insert for 10 secs
amelie bench http://localhost --type=insert --batch=600

# benchmark using previously saved server credentials
amelie bookmark home http://localhost
amelie bench home
```
