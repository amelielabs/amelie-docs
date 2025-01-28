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

Get a system config and current runtime variables.

Same as [SHOW CONFIG](/docs/configuration/show).

```SQL
select system.config().uuid;
["826e3f5d-6ebd-bd08-748d-57eb5e5cd565"]
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

### **`json system.compute()`**

Get a list of created compute nodes in the system.

Same as [SHOW COMPUTE](/docs/compute/show).

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
  "rotate_wm": 104857600,
  "sync_on_rotate": true,
  "sync_on_write": false,
  "lsn": 58,
  "lsn_min": 1,
  "files": 1,
  "slots": 0,
  "slots_min": -1
}]
```

---

### **`json system.status()`**

Show the essential database and process information gathered in one place.

Same as [SHOW STATUS](/docs/monitoring/show).

```SQL
select system.status();
[{
  "uuid": "ad41adcf-6479-f931-a491-2e27272c8a50",
  "version": "1.0.0",
  "hosts": 5,
  "nodes": 11,
  "db": {
    "schemas": 2,
    "tables": 0,
    "tables_shared": 0,
    "secondary_indexes": 0,
  },
  "process": {
    "uptime": 0,
    "mem_virt": 1371725824,
    "mem_resident": 10760192,
    "mem_shared": 5083136,
    "cpu_count": 16,
    "cpu": 26477970,
    "cpu_hosts": [0, 0, 0, 0, 0],
    "cpu_nodes": [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
  },
  "net": {
    "connections": 1,
    "sent_bytes": 0,
    "recv_bytes": 76
  },
  "wal": {
    "active": true,
    "checkpoint": 15627754,
    "lsn": 15627754,
    "lsn_min": 15593964,
    "files": 1,
    "slots": 0,
    "slots_min": -1,
    "writes": 0,
    "writes_bytes": 0,
    "ops": 0
  },
  "repl": {
    "active": false,
    "role": "primary",
    "primary": null,
    "replicas": {}
  }
}]

select system.status().uuid;
["ad41adcf-6479-f931-a491-2e27272c8a50"]
```
