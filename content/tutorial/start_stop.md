---
weight: 3
title: Run Server
bookToc: false
---

## Start Server

The **`amelie start <directory> [options]`** command starts a server.

Optional [server options](/docs/configuration/show) can be passed to the command.

The Server will be started in the current terminal session, waiting for the
**`SIGINT`** (`Ctrl + C`) or **`SIGTERM`** signals to shut down. The **--daemon=true** option can be used to start the
Server in the background. The **`<directory>/pid`** file will be created in both cases, consisting
of the server process ID.

The server creates and keeps the log file **`<directory>/log`**.

During the start, the Server does the following steps:

1) Finds the latest checkpoint and replays partition files in parallel
2) Replays WAL files starting from the latest checkpoint
2) Starts Replication (if configured)
3) Starts accepting incoming connections

By default, the Server runs without authentication and accepts **`HTTP`** connections on the **`3485`** port and a
**`UNIX socket file`** in the directory.

```text
amelie start ./repo
```

## Stop Server

The **`amelie stop <directory>`** command can stop an active server.

```text
amelie stop ./repo
```
