---
weight: 2
title: "SHOW ALL"
bookToc: false
---

## SHOW ALL Statement

```SQL
SHOW ALL
SHOW CONFIG
```

Show configuration and runtime settings.

Most options can be changed only in the configuration file or command line. Some options are read-only and
represent the runtime state.

---

```SQL
show all
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
