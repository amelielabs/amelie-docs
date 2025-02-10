---
weight: 4
title: "System Settings"
bookToc: false
---

## Configuration Settings

Most options can be changed only in the configuration file or command line. Some options are read-only and
represent the runtime state.

Session options can be changed using the [SET](/docs/configuration/set) command.

### Main Settings

| Name              | Type     | Mode      | Description |
| :---------------- | :------: | :----    | :---- |
| uuid              |  string  | cli       | Server ID |
| timezone          |  string  | cli, session | System and session timezone |
| format            |  string  | cli, session | System and session result format |
| shutdown          |  string  | cli          | System shutdown mode: **`fast`** (default) or **`graceful`**.  |

---

```SQL
show uuid;
["a74fbf39-cc9d-314e-a33e-3aa47559ffe5"];

select system.config().uuid;
["a74fbf39-cc9d-314e-a33e-3aa47559ffe5"]

show format;
["json-pretty"]
```

### Logger Settings

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----       | :---- |
| log_enable        |  bool    | cli | Log messages |
| log_to_file       |  bool    | cli  | Write log messages to file inside the base directory |
| log_to_stdout     |  bool    | cli | Duplicate log message to stdout |
| log_connections   |  bool    | cli | Log connect/diconnect client events |
| log_options       |  bool    | cli | Log configuration options on start |

---

```SQL
show log_connections;
[true]
```

### TLS Certificates

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----       | :---- |
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

### Server Settings

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----       | :---- |
| listen            |  array   | cli          | Listen for incoming connections |

Listen represent an array of objects, where following fields are recognized:

| Argument             | Type | Description |
| :----------------    |  :----  | :----      |
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

### Session Limits

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----       | :---- |
| limit_send        |  int     | cli | Limit for reply (bytes) |
| limit_recv        |  int     | cli | Limit for request (bytes) |
| limit_write       |  int     | cli | Limit for transaction log size (bytes) |

---

```SQL
show limit_send;
[3145728]

show limit_recv;
[1048576]

show limit_write;
[0]
```

### IO and Compute Workers

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----       | :---- |
| frontends         |  int     | cli          | Number of frontend workers |
| backends          |  int     | init cli     | Number of backend workers. Can be changed only once on init, after that the DDL commands must be used |

---

```SQL
show frontends;
[5]
```

### WAL Settings

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----       | :---- |
| wal_size          |  int     | cli | The number of operations per WAL file. When the current WAL file reaches this value, a new file will be created |
| wal_sync_on_rotate |  bool   | cli | Sync the previous WAL file when a new one is created (enabled by default) |
| wal_sync_on_write |  bool    | cli | Sync the current WAL file on each write (disabled by default) |

### Replication Settings

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----       | :---- |
| repl_reconnect_ms |  int     | cli | Reconnect interval in ms |


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

### Checkpoint

| Name                | Type     | Mode         | Description |
| :----------------   | :------: | :----       | :---- |
| checkpoint_interval | interval | cli          | 5 minutes by default |
| checkpoint_workers  | int      | cli          | Number of workers which will be created during checkpoint (3 by default) |
