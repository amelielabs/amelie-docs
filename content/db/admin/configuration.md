---
weight: 18
title: "Configuration"
bookToc: true
---

# Configuration Settings

Following options can be changed in the configuration file **`<directory>/config.json`**
or passed in the command line on start.

Options passed during repository creation will be saved in the configuration file.

All system information stored and presented in JSON.

```SQL
SHOW ALL;

config
──────
{
  "uuid": "b9b6fbf1-85de-9a0b-63e2-3233e03c6803",
  "timezone": "Asia/Famagusta",
  "log_enable": true,
  "log_file": true,
  "log_stdout": true,
  "log_stdout_time": true,
  "log_connections": true,
  "log_options": false,
  "limit_send": 3145728,
  "limit_recv": 1048576,
  "limit_write": 0,
  "frontends": 4,
  "backends": 6,
  "jobs": 3,
  "cpu_affinity": true,
  "wal_crc": true,
  "wal_sync_create": true,
  "wal_sync_close": true,
  "wal_sync_write": false,
  "wal_sync_interval": "1 sec",
  "wal_service": true,
  "wal_size": 67108864,
  "wal_checkpoint": 100,
  "wal_rewind": false,
  "wal_rewind_pos": 0,
  "storage_crc": true,
  "storage_sync": true,
  "catalog_sync": true,
  "repl_readahead": 262144,
  "repl_reconnect_ms": 3000
}
```

#### Main Settings

| Name              | Type     | Description |
| :---------------- | :------: | :---- |
| uuid              |  string  | Server ID |
| timezone          |  string  | System and session default timezone |

---

```SQL
SHOW uuid;

uuid
────
"b9b6fbf1-85de-9a0b-63e2-3233e03c6803"

SELECT show().uuid;

uuid
────
"b9b6fbf1-85de-9a0b-63e2-3233e03c6803"
```

#### Logger Settings

| Name              | Type     | Description |
| :---------------- | :------: | :---- |
| log_enable        |  bool    | Log messages |
| log_file          |  bool    | Write log messages to file inside the base directory |
| log_stdout        |  bool    | Duplicate log message to the stdout |
| log_stdout_time   |  bool    | Include timestamps in the stdout output |
| log_connections   |  bool    | Log connect/diconnect client events |
| log_options       |  bool    | Log configuration options on start |

---

```SQL
SHOW log_connections;

log_connections
───────────────
true
```

#### Session Limits

| Name              | Type     | Description |
| :---------------- | :------: |  :---- |
| limit_send        |  int     | Limit for reply (bytes) |
| limit_recv        |  int     | Limit for request (bytes) |
| limit_write       |  int     | Limit for transaction log size (bytes) |

---

```SQL
SHOW limit_send;

limit_send
──────────
3145728
```

#### IO and Compute Workers

| Name              | Type     | Description |
| :---------------- | :------: | :---- |
| frontends         |  int     | Number of frontend workers |
| backends          |  int     | Number of backend workers |

---

#### WAL Settings

| Name              | Type     | Description |
| :---------------- | :------: | :---- |
| wal_crc           |  bool    | Calculate and validate checksums during WAL write and read (enabled by default). |
| wal_sync_on_create |  bool   | Sync the WAL file together with the directory after creation (enabled by default). |
| wal_sync_on_close |  bool    | Sync the WAL file before closing (enabled default). |
| wal_sync_on_write |  bool    | Sync the WAL file on each write (disabled by default). |
| wal_sync_interval |  string  | Sync the WAL file every interval ("1 sec" by default). |
| wal_service       |  bool    | Do WAL fsync() and other service tasks in other worker thread (enabled by default). |
| wal_size          |  int     | When the current WAL file reaches this value, a new file will be created. |
| wal_checkpoint    |  int     | Do automatic CHECKPOINT on reaching this file count (Default is 100). |
| wal_rewind        |  bool    | Truncate WAL files to the specified LSN value to recover invalid WAL files and bring them to a valid location after a crash. This operation is potentially dangerous. To proceed, it is recommended that you create a copy of the WAL data first. |
| wal_rewind_pos    |  int     | Truncate WAL LSN position. |

#### Replication Settings

| Name              | Type     | Description |
| :---------------- | :------: | :---- |
| repl_readahead    |  int     | The amount of data to read from WAL in bytes before sending it to the replica. |
| repl_reconnect_ms |  int     | Reconnect interval in ms |


#### Storage

| Name              | Type     | Description |
| :---------------- | :------: | :---- |
| storage_crc       |  bool    | Calculate and validate storage/checkpoint checksums (enabled by default). |
| storage_sync      |  bool    | Sync the partition files (enabled by default). |
| catalog_sync      |  bool    | Sync the catalog file (enabled by default). |
