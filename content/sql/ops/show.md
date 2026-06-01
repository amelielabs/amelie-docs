---
weight: 7
title: "SHOW"
bookToc: true
---

# SHOW

```SQL
SHOW [ALL] [section] [name] [ON name] [VERBOSE]
```

Show system configuration, state and catalog infromation. 

All listed below show commands are available during either by calling [show()](/docs/sql/builtin/show)
or in a form of [SELECT FROM SHOW](/docs/sql/ops/query/select).

The **`ALL`** clause (except for SHOW ALL) allows to additionally include relations that were shared
with the current user (has grants).

### Relations

```SQL
SHOW [ALL] RELS
SHOW REL name [VERBOSE]
```

### Tables

```SQL
SHOW [ALL] TABLES [VERBOSE]
SHOW TABLE name [VERBOSE]
```

```SQL
SHOW INDEXES ON table_name [VERBOSE]
SHOW INDEX name ON table_name [VERBOSE]
```

```SQL
SHOW PARTITIONS ON table_name [VERBOSE]
SHOW PARTITION 'id' ON table_name [VERBOSE]
```

### Clones

```SQL
SHOW [ALL] CLONES
SHOW CLONE name [VERBOSE]
```

### Topics

```SQL
SHOW [ALL] TOPICS
SHOW TOPIC name [VERBOSE]
```

### Subscriptions

```SQL
SHOW [ALL] SUBSCRIPTIONS
SHOW SUBSCRIPTION name [VERBOSE]

SHOW SUBS
SHOW SUB name [VERBOSE]
```

### User-Defined Functions

```SQL
SHOW [ALL] FUNCTIONS
SHOW FUNCTION name [VERBOSE]
```

### Grants

```SQL
SHOW GRANTS ON rel_name [VERBOSE]
```

### Users

```SQL
SHOW [ALL] USERS
SHOW USER name [VERBOSE]
```

### Replication

```SQL
SHOW REPLICAS
SHOW REPLICA name [VERBOSE]
```

```SQL
SHOW REPLICATION [VERBOSE]
SHOW REPL [VERBOSE]
```

### Configuration

```SQL
SHOW ALL
SHOW CONFIG
```

### System

```SQL
SHOW STATE
SHOW WAL
SHOW METRICS
SHOW LOCKS
```
