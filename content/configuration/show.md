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
  "uuid": "654205bb-38f6-2aca-266b-903cef964563",
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
  "wal_worker": true,
  "wal_crc": true,
  "wal_sync_on_create": true,
  "wal_sync_on_close": true,
  "wal_sync_on_write": false,
  "wal_sync_interval": "1 sec",
  "wal_size": 67108864,
  "wal_truncate": 0,
  "repl_readahead": 262144,
  "repl_reconnect_ms": 3000,
  "checkpoint_interval": "5 min",
  "checkpoint_workers": 3
}]

select system.config().uuid;
["654205bb-38f6-2aca-266b-903cef964563"]
```
