---
weight: 10
title: Benchmarking
bookToc: false
---

## Benchmarking

The **`amelie bench [login] [client options] [bench options]`** command can be used for server benchmarking
using predefined tests. The command is compatible with the [Console Client](/docs/tutorial/cli) options.

The following benchmarking options are supported:

| Argument          | Type | Description |
| :---------------- |  :----:  | :----      |
| type          | string | Benchmark type: **`tpcb`** (default), **`insert`**, **`upsert`**, **`resolved`**, **`import`**, **`decre`**. |
| threads       | int | Number of client threads (default is 1). |
| clients       | int | Total number of clients (default is 12). |
| time          | int | Time in seconds (default is 10). |
| batch         | int | Number of rows in one insert/upsert statement (default is 500). |
| scale         | int | The scale factor for `tpcb` test (default is 1). |
| init          | bool | Prepare tables for testing (default is true). |
| unlogged      | bool | Mark tables as unlogged (default is false). |

### TPC-B Style Benchmark

This is the default benchmarking type, made to match the [PostgreSQL pgbench](https://www.postgresql.org/docs/current/pgbench.html) command to get an exact
performance comparison with PostgreSQL.

It continuously executes the following multi-statement transaction, which involves four tables.

```SQL
begin

update accounts
set abalance = abalance + :delta
where aid = :aid;

select abalance into :abalance
from accounts
where aid = :aid;

update tellers
set tbalance = tbalance + :delta
where tid = :tid;

update branches
set bbalance = bbalance + :delta
where bid = :bid;

insert into history(tid, bid, aid, delta, time)
values (:tid, :bid, :aid, :delta, current_timestamp);

commit
```

### Insert Benchmark

Sequentially Insert rows using the [INSERT](/docs/sql/dml/insert) statement. The number of rows per one operation can be configured using
the **`batch`** option. The test table's primary index is **`tree`**.

Watch out for available RAM.

### Upsert Benchmark

Randomly Insert rows using the [INSERT ON CONFLICT DO UPDATE](/docs/sql/dml/insert) statement. The number of rows per one operation
can be configured using the **`batch`** option. The test table's primary index is **`hash`**.

The number of rows in the table is set to 100000 random keys.

### Resolved Benchmark

Randomly Insert rows where each column is generated as **`stored`** or **`resolved`** together. The number of rows per one operation
can be configured using the **`batch`** option. The test table's primary index is **`hash`**.

```SQL
create table __bench.test (
  ts   timestamp as ( current_timestamp::date_bin('3 sec'::interval) ) stored,
  id   int random (10000),
  hits int default 0 as ( hits + 1 ) resolved,
  primary key(ts, id)
) with (type = 'hash');
```

### Import Benchmark

Sequentially stream rows using the [HTTP API](/docs/api/import_json). The number of rows per one operation can be configured using
the **`batch`** option. The test table's primary index is **`tree`**.

Watch out for available RAM.

### Debit/Credit Benchmark

Execute basic financial transactions which include two update. The number of transactions per one round-trip can be configured using
the **`batch`** option (try lower values). The test table's primary index is **`hash`**.

### Recommendations

Please note that the number of **`frontends`**, **`backends`** in the system, as well as using **`unlogged`** tables directly
impact the performance. It is a good idea to start with defaults and then alter the numbers
to see how is affects the performance.

More is not always better, especially if you are running benchmarks on the same machine. There is a possible
situation when workers will start competing for CPU cores and locking each other.

[Learn more](/docs/compute/overview) about the IO and Compute.

### Third-Party Benchmarking tools

Using any HTTP benchmarking tool configured to generate custom requests is possible.

Please ensure the benchmarking tool can adequately adjust the pressure level to match the processing capabilities.

One such tool is [wrk](https://github.com/wg/wrk/tree/master).

---

```sh
# do tpcb style benchmark for 1 minute
amelie bench --uri="http://localhost:3485" --time=60

# do batch insert for 10 secs
amelie bench --uri="http://localhost:3485" --type="insert" --batch=600

# benchmark using previously saved server credentials
amelie login home --uri="http://localhost:3485"
amelie bench home
```
