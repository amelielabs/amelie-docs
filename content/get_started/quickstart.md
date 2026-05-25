---
weight: 1
title: Quickstart
bookToc: true
---

# Get Started

Amelie is distributed as a single executable binary **`amelie`**. It provides the functionality of the **Server**,
**Console Client**, **Backup** and **Benchmark** tool:

Please look at the [Build and Install](/docs/db/admin/build) section for the manual build instructions.

## Deploy a Database

{{% steps %}}
1. [Create](/docs/db/admin/create)
   ```sh
   amelie init ./repo
   ```
2. [Run](/docs/db/admin/start_stop)
   ```sh
   amelie start ./repo
   ```

3. [Connect](/docs/db/admin/cli)
    ```sh
    # connect using 8080 port (default)
    amelie http://localhost

    # connect using unixsocket
    amelie ./repo
    ```
{{% /steps %}}


## Develop with Amelie

Create your applications using [SQL](/docs/sql/overview) and the [HTTP API](/docs/api/http), [JSON-RPC API](/docs/api/jsonrpc).
Alternatively, use the [Embedded API](/docs/api/embedded) to access Amelie within your application.

## Setup external connections

For security reasons, external connections must be [configured manually](/docs/db/admin/create)
and will require:

{{% steps %}}
1. [Create Users and Agents](/docs/db/admin/auth)
2. [Configure TLS certificates](/docs/db/admin/tls)
{{% /steps %}}

## Maintain

A typical server Maintenance should include:

* [Monitoring](/docs/db/admin/monitoring)
* [Periodic Backups](/docs/db/admin/backup)

Additionally, it is possible to setup [Replication](/docs/sql/ddl/repl/overview).
