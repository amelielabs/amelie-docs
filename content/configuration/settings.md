---
weight: 4
title: "System Settings"
bookToc: false
---

## Configuration and Runtime Settings

Most options can be changed only in the configuration file or command line. Some options are read-only and
represent the runtime state.

Dynamic options can be changed using the [SET](/docs/configuration/set) command, which might update
the configuration file.

## Main Settings

| Name              | Type     | Mode      | Description |
| :---------------- | :------: | :----:    | :---- |
| version           |  string  | read-only | Server version |
| uuid              |  string  | cli       | Server ID |
| directory         |  string  | read-only | Base directory |
| timezone_default  |  string  | cli       | Default server timezone |
| timezone          |  string  | session   | Session timezone, set to `timezone_default` if not defined |
| format            |  string  | session   | Session result format |

---

```SQL
show uuid;
["a74fbf39-cc9d-314e-a33e-3aa47559ffe5"];

select system.config().uuid;
["a74fbf39-cc9d-314e-a33e-3aa47559ffe5"]

show format;
["json-pretty"]
```

## Logger Settings

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----:       | :---- |
| log_enable        |  bool    | cli          | Log messages |
| log_to_file       |  bool    | cli          | Write log messages to file inside the base directory |
| log_to_stdout     |  bool    | cli          | Duplicate log message to stdout |
| log_connections   |  bool    | cli, session | Log connect/diconnect client events |

---

```SQL
show log_connections;
[true]
```

## TLS Certificates

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----:       | :---- |
|  tls_capath      | string | cli | TLS CA directory path. |
|  tls_ca          | string | cli | TLS CA certificate file path. |
|  tls_cert        | string | cli | TLS Server certificate file path. |
|  tls_key         | string | cli | TLS Server certificate private key file path. |

---

```SQL
show tls_cert;
[""]

select system.config().tls_cert;
[""]
```

## Server Settings

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----:       | :---- |
| listen            |  array   | cli          | Listen for incoming connections |

Listen represent an array of objects, where following fields are recognized:

| Argument             | Type | Description |
| :----------------    |  :----:  | :----      |
|  path            | string | Unix socket file path. |
|  path_mode       | string | Unix socket file mode. |
|  host            | string | Listen address (using **`host`** or **`path`** is mandatory). |
|  port            | int    | Listen port. |
|  tls             | bool    | Enable TLS for this address. |
|  auth            | bool    | Enable Authentication for this address. |

---


```SQL
show listen;
[{
  "host": "*",
  "port": 3485,
  "auth": true,
  "tls": true
}]

select system.config().listen;
[{
  "host": "*",
  "port": 3485,
  "auth": true,
  "tls": true
}]
```

## Session Limits

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----:       | :---- |
| limit_send        |  int     | cli, session | Limit for reply (bytes) |
| limit_recv        |  int     | cli, session | Limit for request (bytes) |
| limit_write       |  int     | cli, session | Limit for transaction log size (bytes) |

---

```SQL
show limit_send;
[3145728]

show limit_recv;
[1048576]

show limit_write;
[0]
```

## Cluster Settings

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----:       | :---- |
| hosts             |  int     | cli          | Number of hosts workers |
| nodes             |  int     | init cli     | Number of compute nodes |

---

```SQL
show hosts;
[5]

show nodes;
[12]
```

## WAL Settings

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----:       | :---- |
| wal_rotate_wm     |  int     | cli, session | The number of operations per WAL file. When the current WAL file reaches this value, a new file will be created |
| wal_sync_on_rotate |  bool   | cli | Sync the previous WAL file when a new one is created (enabled by default) |
| wal_sync_on_write |  bool    | cli | Sync the current WAL file on each write (disabled by default) |

---

```SQL
show wal;
[{
  "active": true,
  "rotate_wm": 104857600,
  "sync_on_rotate": true,
  "sync_on_write": false,
  "lsn": 210,
  "lsn_min": 1,
  "files": 2,
  "slots": 1,
  "slots_min": -1
}]
```

## Replication Settings

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----:       | :---- |
| repl              |  bool    | cli          | Enable/Disable replication (disabled by default) |
| repl_primary      |  string  | cli          | Replication primary server ID |
| repl_reconnect_ms |  int     | cli, session | Reconnect interval in ms |

Variables **`repl`** and **`repl_primary`** are changed automatically by the replication commands.

---

```SQL
show repl_reconnect_ms;
[3000]

show repl;
[{
  "active": false,
  "role": "primary",
  "primary": null
}]
```

## Checkpoint

| Name                | Type     | Mode         | Description |
| :----------------   | :------: | :----:       | :---- |
| checkpoint_interval | interval | cli          | 5 minutes by default |
| checkpoint_workers  | int      | cli          | Number of workers which will be created during checkpoint (3 by default) |
| checkpoint          | int      | cli          | Last checkpoint LSN |

---

```SQL
show checkpoint;
[56]
```

## System State

| Name                | Type     | Mode         | Description |
| :----------------   | :------: | :----:       | :---- |
| read_only           | bool     |  read-only   | System in read-only mode cannot accept writes |
| lsn                 | int      |  read-only   | Log Sequence Number |
| psn                 | int      |  read-only   | Partition Sequence Number  |

---

```SQL
show lsn;
[56]
```
