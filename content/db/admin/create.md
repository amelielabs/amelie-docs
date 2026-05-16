---
weight: 3
title: Create Repository
bookToc: true
---

# Create Repository

The **`amelie init <directory> [options]`** command is used to create a database repository.

Optional [server options](/docs/db/admin/configuration/settings) can be passed to the command.

Options passed during repository creation will be saved in the configuration file, which will be created
inside the directory: **`<directory>/config.json`**

```text
amelie init ./repo
```

Server options can be changed directly by modifying the configuration file when the server is not
running or passed to the **`amelie start`**.

## Initial Configuration

Several essential options can be passed directly to the **`amelie init`** command or changed after
creating the repository.

The most important options are:

| Argument             | Type | Description |
| :---------------- |  :----:  | :----      |
| uuid              | string | Set server UUID. If not provided, it will be generated automatically. |
| timezone  | string | Timezone to use. If not provided, the system timezone will be used. |
| frontends         | int | The number of frontend workers. It will be set automatically based on the number of CPU cores if not provided. |
| backends          | int | The number of pre-created backend workers. It will be set automatically based on the number of CPU cores if not provided. |

By default, the server configured to accepts **`HTTP`** connections on port **`8080`** and the **`UNIX socket file`**
created in the repository.

## Remote Connections

For security reasons, Amelie will listen only on the **`localhost`** addresses. Local connections
considered secure will be allowed to connect as the **`amelie`** superuser without
authentication.

External connections must be configured manually in **`<directory>/server.json`** config file.
	
All external connections must include valid [TLS certificates](/docs/db/admin/tls) and will require to create
additional [Users and Agents](/docs/db/admin/auth) with valid authentication tokens.

It is forbidded to use **`amelie`** superuser in remote connections.

## IO and Compute workers

Options **frontends**, **backends** directly impact the performance. They can be also changed at the server start.

[Learn more](/docs/db/architecture/overview) about the IO and Compute processing.

---

```sh
# create repository and run the server
amelie init ./repo --backends=6 --frontends=4
amelie start ./repo

# connect using http
amelie http://localhost

# connect using unixsocket
amelie ./repo
```
