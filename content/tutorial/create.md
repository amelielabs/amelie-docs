---
weight: 3
title: Create Repository
bookToc: false
---

## Create Repository

The **`amelie init <directory> [options]`** command is used to create a database repository.

Optional [server options](/docs/configuration/show) can be passed to the command. Options passed during
repository creation will be saved in the configuration file, which will be created inside the directory:
**`<directory>/config.json`**

```text
amelie init ./repo
```

Server options can be changed directly by modifying the configuration file when the server is not
running. Please note that the server dynamically updates the configuration file and keeps the information
about users and replicas.

Some options can be changed dynamically using the [SET](/docs/configuration/set) command or passed to
the **`amelie start`**.

### Initial Configuration

Several essential options can be passed directly to the **`amelie init`** command or changed after
creating the repository.

The most notable options are:

| Argument             | Type | Description |
| :---------------- |  :----:  | :----      |
| uuid              | string | Set server UUID. If not provided, it will be generated automatically. |
| default_timezone  | string | Timezone to use. If not provided, the system timezone will be used. |
| hosts             | int | The number of hosts workers. It will be set automatically based on the number of CPU cores if not provided. |
| nodes             | int | The number of pre-created compute nodes. It will be set automatically based on the number of CPU cores if not provided. |
| listen            | array | List of the addresses to accept connections. By default, it accepts all connections without authentication. |


The [listen](/docs/configuration/settings) option can be configured to accept connections from different network addresses,
with or without authentication, with or without using the [TLS certificates](/docs/configuration/settings).

## Cluster Configuration

Options **hosts**, **nodes** and using **`unlogged`** tables directly impact the server performance.

The number of **hosts** workers can be changed at the server start, and the number of **nodes** workers (compute nodes)
can be modified later using the [ALTER COMPUTE](/docs/compute/alter) command.

[Learn more](/docs/compute/overview) about the Cluster.
