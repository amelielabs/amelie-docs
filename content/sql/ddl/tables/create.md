---
weight: 1
title: "CREATE TABLE"
bookToc: false
---

## CREATE TABLE Statement

```SQL
CREATE [SHARED|DISTRIBUTED] TABLE [IF NOT EXISTS] [schema.]name
(column [, ...] [, primary key (keys)])
[WITH (options)]

column:
	name type [constraints]

type:
	int
	real
	bool
	text
	object	
	array
	timestamp
	interval
	vector

constraints:
	NOT NULL
	DEFAULT const
	SERIAL
	PRIMARY KEY

primary key:
	PRIMARY KEY [(column name | [path type], ...)] 

options:
	name = expr [,...]
```

Create a new table object if it does not exist.

Tables store rows in the format of arrays according to the defined column types of the tables.

If the schema name is not defined, it will be set to **`public`** by default. One or more columns must be
defined as a **`PRIMARY KEY`**. Currently, only **`INT`**, **`STRING`**, and **`TIMESTAMP`** columns can be used as
part of a key.

The table **`primary`** index will be automatically created using a defined index type and the primary key.
The primary index is always created as **`UNIQUE`**. Supported index types are **`hash`** and **`tree`**. The index type can
be selected using the **`WITH`** clause. If the index type is not defined, it will default to **`tree`**.

All tables are automatically partitioned (hash partitioning), and partitions are created on one or
more nodes. Amelie uses consistent hashing to assign each partition interval to a node. **`PRIMARY KEY`**
columns are used as the partition key.

Currently, the **`CREATE TABLE`** operation cannot be part of multi-statement transactions.

There are two types of tables: **`DISTRIBUTED`** and **`SHARED`**.

### Distributed Tables

By default, all tables are **`distributed`**, meaning each distributed table will have partitions
created on each node for parallel access or modification. Currently, distributed tables cannot
be used directly in a JOIN with other distributed tables. However, they can be used in a multi-statement
transaction or [CTE](/docs/sql/transactions/cte).

### Shared Tables

There is also a particular type of table called **`shared`**. Those tables have only one partition and are
available for direct read access from any node. They can be used to implement efficient **`parallel
JOIN`** operations with other distributed tables. Frequent updating of a shared table is
less efficient since it requires coordination and exclusive access.

### Relational vs. Document Tables

Instead of following traditional relational approach of adding and dropping new columns,
organizing tables by separating and creating volatile columns as document values (objects and arrays) or ultimately
moving to store objects (schemaless) is recommended.

### Schemaless Tables

Sometimes, the relational table structure is highly volatile, and it would be easier to
store JSON objects directly. Amelie supports tables that can store and build indexes on a single
JSON column with a variable structure for such cases.

---

```SQL
-- Table stores and returns rows as JSON arrays
create table metrics (
  device_id int primary key,
  data array
)
insert into metrics values (42, [1,2,3])

select * from metrics
[[42, [1, 2, 3]]]

select data from metrics
[[1, 2, 3]]

-- JSON expressions
select {"id": device_id, "sensors": data} from metrics
[{
  “id”: 42,
  "sensors": [1, 2, 3]
}]
```

```SQL
create table schemaless (obj object, primary key (obj.id int))
insert into schemaless {"id": 48, "data": [1,2,3]}, {"id": 56}
select obj from schemaless where obj::has("data")
[{
  "id": 48,
  "data": [1, 2, 3]
}]
```

```SQL
create table test (id int primary key) with (type = 'hash')
create table test (id int primary key) with (type = 'tree')
```
