---
weight: 1
title: "System"
bookToc: false
---

## System Functions

All system functions are located in the **`system`** schema.

Following system functions are aliases for corresponding [SHOW](/docs/tutorial/monitoring) commands.

### system.config()

Get a system config and current runtime variables.

Same as [SHOW CONFIG](/docs/configuration/show).

```SQL
select system.config()
[{
  "version": "1.0",
  "uuid": "0f49c30f-5cf5-ee72-f3d7-8bfadbaea495",
  "directory": "t",
  "timezone": "Asia/Famagusta",
  "timezone_default": "Asia/Famagusta",
  "log_enable": true,
  "log_to_file": true,
  "log_to_stdout": true,
  "log_connections": true,
  "tls_capath": "",
  "tls_ca": "",
  "tls_cert": "",
  "tls_key": "",
  "listen": [{
    "host": "*",
    "port": 3485
  }],
  "limit_send": 3145728,
  "limit_recv": 1048576,
  "limit_write": 0,
  "frontends": 5,
  "backends": 11,
  "wal": true,
  "wal_rotate_wm": 104857600,
  "wal_sync_on_rotate": true,
  "wal_sync_on_write": false,
  "repl": false,
  "repl_primary": "",
  "repl_reconnect_ms": 3000,
  "checkpoint_interval": "5 min",
  "checkpoint_workers": 3,
  "checkpoint": 0,
  "read_only": false,
  "lsn": 173943,
  "psn": 22
}]

select system.config().uuid
["0f49c30f-5cf5-ee72-f3d7-8bfadbaea495"]
```
---

### system.users()

Get a list of users.

Same as [SHOW USERS](/docs/users/show).

```SQL
select system.users()
[{
  "name": "test"
}]

select system.users().test
[{
  "name": "test"
}]

select name from system.users()
["test"]
```

---

### system.replicas()

Get a list of created replicas in the system.

Same as [SHOW REPLICAS](/docs/repl/show_replicas).

---

### system.repl()
### system.replication()

Get the replication status.

Same as [SHOW REPL](/docs/repl/show) or [SHOW REPLICATION](/docs/repl/show).

```SQL
select system.repl()
[{
  "active": false,
  "role": "primary",
  "primary": null
}]
```

---

### system.nodes()

Get a list of created nodes in the system.

Same as [SHOW NODES](/docs/cluster/show).

---

### system.schemas()

Get a list of created schemas.

Same as [SHOW SCHEMAS](/docs/sql/ddl/schemas/show).

---

### system.tables()

Get a list of created tables.

Same as [SHOW TABLES](/docs/sql/ddl/tables/show).

---

### system.views()

Get a list of created views.

Same as [SHOW VIEWS](/docs/sql/ddl/views/show).

---

### system.wal()

Get the WAL status.

Same as [SHOW WAL](/docs/storage/show).

```SQL
select system.wal()
[{
  "active": true,
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
