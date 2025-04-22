---
weight: 14
title: "System"
bookToc: false
---

## System Functions

All system functions are located in the **`system`** schema.

Following system functions are aliases for corresponding [SHOW](/docs//monitoring/overview) commands.

---

### **`json system.config()`**

Get a system config.

Same as [SHOW CONFIG](/docs/configuration/show).

```SQL
select system.config().uuid;
["826e3f5d-6ebd-bd08-748d-57eb5e5cd565"]
```

---

### **`json system.state()`**

Get a system state information.

Same as [SHOW STATE](/docs/monitoring/show_state).

```SQL
select system.state()
[{
  "version": "0.1.0",
  "directory": "./test_repo",
  "uuid": "cd580566-6cf7-fb90-737d-50dd8abdbc79",
  "frontends": 8,
  "backends": 8,
  "checkpoint": 1,
  "lsn": 1,
  "psn": 0,
  "read_only": false
}]
```
---

### **`json system.users()`**

Get a list of users.

Same as [SHOW USERS](/docs/users/show).

```SQL
select system.users();
[{
  "name": "test"
}]

select system.users().test;
[{
  "name": "test"
}]
```

---

### **`json system.user(string)`**

Show user information.

Same as [SHOW USER](/docs/users/show).

```SQL
select system.user('test').name;
["test"]
```

---

### **`json system.replicas()`**

Get a list of created replicas in the system.

Same as [SHOW REPLICAS](/docs/repl/show_replica).

---

### **`json system.replica(string)`**
### **`json system.replica(uuid)`**

Get the status of a replica.

Same as [SHOW REPLICA](/docs/repl/show_replica).

```SQL
select system.replica('00000000-0000-0000-0000-000000000001').uri;
["http://localhost:3481"]
```

---

### **`json system.repl()`**
### **`json system.replication()`**

Get the replication status.

Same as [SHOW REPL](/docs/repl/show) or [SHOW REPLICATION](/docs/repl/show).

```SQL
select system.repl();
[{
  "active": false,
  "role": "primary",
  "primary": null
}]
```

---

### **`json system.backends()`**

Get a list of created backend workers in the system.

Same as [SHOW BACKENDS](/docs/compute/show).

---

### **`json system.schemas()`**

Get a list of created schemas.

Same as [SHOW SCHEMAS](/docs/sql/ddl/schemas/show).

---

### **`json system.schema(string)`**

Show schema information.

Same as [SHOW SCHEMA](/docs/sql/ddl/schemas/show).

```SQL
select system.schema('example').system;
[false]
```

---

### **`json system.tables()`**

Get a list of created tables.

Same as [SHOW TABLES](/docs/sql/ddl/tables/show).

---

### **`json system.table(string)`**

Show table information.

Same as [SHOW TABLE](/docs/sql/ddl/tables/show).

```SQL
select system.table('example').columns;
[[{
  "name": "primary",
  "type": 2,
  "unique": true,
  "primary": true,
  "keys": [{
    "column": 0
  }]
}]]
```

---


### **`json system.wal()`**

Get the WAL status.

Same as [SHOW WAL](/docs/reliability/show).

```SQL
select system.wal();
[{
  "lsn": 1,
  "lsn_min": 1,
  "files": 1,
  "slots": 0,
  "slots_min": -1,
  "writes": 0,
  "writes_bytes": 0,
  "ops": 0,
  "checkpoint": 1
}]
```

---

### **`json system.metrics()`**

Show the essential database and process information gathered in one place.

Same as [SHOW METRICS](/docs/monitoring/show).

```SQL
select system.metrics();
[{
  "uuid": "cd580566-6cf7-fb90-737d-50dd8abdbc79",
  "version": "0.1.0",
  "frontends": 8,
  "backends": 8,
  "db": {
    "schemas": 2,
    "tables": 0,
    "secondary_indexes": 0
  },
  "process": {
    "uptime": 0,
    "mem_virt": 1371512832,
    "mem_resident": 10932224,
    "mem_shared": 5267456,
    "cpu_count": 16,
    "cpu": 22891059,
    "cpu_frontends": [0, 0, 0, 0, 0, 0, 0, 0],
    "cpu_backends": [0, 0, 0, 0, 0, 0, 0, 0]
  },
  "net": {
    "connections": 1,
    "sent_bytes": 0,
    "recv_bytes": 77
  },
  "wal": {
    "lsn": 1,
    "lsn_min": 1,
    "files": 1,
    "slots": 0,
    "slots_min": -1,
    "writes": 0,
    "writes_bytes": 0,
    "ops": 0,
    "checkpoint": 1
  },
  "repl": {
    "active": false,
    "role": "primary",
    "primary": null,
    "replicas": []
  }
}]

select system.metrics().uuid;
["cd580566-6cf7-fb90-737d-50dd8abdbc79"]
```
