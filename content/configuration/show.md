---
weight: 2
title: "SHOW CONFIG"
bookToc: false
---

## SHOW CONFIG Statement

```SQL
SHOW CONFIG [FORMAT type]
SHOW ALL [FORMAT type]
```

Show configuration settings.

Most options can be changed only in the configuration file or command line.

The [FORMAT](/docs/sql/query/format) clause can be used to specify the format of the result.

---

```SQL
show config
[{
  "uuid": "cd580566-6cf7-fb90-737d-50dd8abdbc79",
  "timezone": "Asia/Famagusta",
  "format": "json-pretty",
  "shutdown": "fast",
  "log_enable": true,
  "log_to_file": true,
  "log_to_stdout": true,
  "log_connections": true,
  "log_options": false,
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
  "wal_size": 67108864,
  "wal_sync_on_rotate": true,
  "wal_sync_on_write": false,
  "repl_reconnect_ms": 3000,
  "checkpoint_interval": "5 min",
  "checkpoint_workers": 3
}]

select system.config().uuid;
["cd580566-6cf7-fb90-737d-50dd8abdbc79"]
```
