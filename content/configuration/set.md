---
weight: 3
title: "SET"
bookToc: false
---

## SET Statement

```SQL
SET name TO value
```

Change configuration and runtime settings.

Most options can be changed only in the configuration file or command line. Some options are read-only and
represent the runtime state.

---

```SQL
show all
[{
  "version": "1.0.0",
  "uuid": "826e3f5d-6ebd-bd08-748d-57eb5e5cd565",
  "directory": "t",
  "timezone": "Asia/Famagusta",
  "timezone_default": "Asia/Famagusta",
  "format": "json-pretty",
  "log_enable": true,
  "log_to_file": true,
  "log_to_stdout": true,
  "log_connections": true,
  "log_options": true,
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
  "frontends": 8,
  "backends": 8,
  "wal": false,
  "wal_rotate_wm": 104857600,
  "wal_sync_on_rotate": true,
  "wal_sync_on_write": false,
  "repl": false,
  "repl_primary": "",
  "repl_reconnect_ms": 3000,
  "checkpoint_interval": "5 min",
  "checkpoint_workers": 3,
  "checkpoint": 12,
  "read_only": false,
  "lsn": 12,
  "psn": 25
}]

set timezone to 'UTC'
```
