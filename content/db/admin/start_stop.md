---
weight: 3
title: Run Server
bookToc: true
---

# Run Server

## Start Server

The **`amelie start <directory> [options]`** command starts a server.

Optional [server options](/docs/db/admin/configuration) can be passed to the command.

The Server will be started in the current terminal session, waiting for the
**`SIGINT`** (`Ctrl + C`) or **`SIGTERM`** signals to shut down. The **--daemon=true** option can be used to start the
Server in the background. The **`<directory>/pid`** file will be created in both cases, consisting
of the server process ID.

The server creates and keeps the log file **`<directory>/log`**.

During the start, the Server does the following steps:

{{% steps %}}
1. Reads the catalog file and loads partition files in parallel
2. Replays WAL files
3. Starts Replication (if configured)
4. Starts accepting incoming connections
{{% /steps %}}

```text
amelie start --daemon=true ./repo
```

## Stop Server

The **`amelie stop <directory>`** command can stop an active server.

```text
amelie stop ./repo
```
