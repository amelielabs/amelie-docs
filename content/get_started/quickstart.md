---
weight: 1
title: Quickstart
bookToc: true
---

# Get Started

Amelie is distributed as a single executable file. It provides the functionality of the **Server**,
**Console Client**, **Backup** and **Benchmark** tool:

```text
> amelie --help
Usage: amelie [PATH | URI | BOOKMARK] [command] [OPTIONS]

Commands:
  init       Create database repository
  start      Start database
  stop       Stop database
  backup     Create database backup
  import     Import data files into the database
  bookmark   Create, update or delete bookmark
  bench      Run benchmarks
  test       Run tests
  test_slt   Run slt tests
```

Please look at the [Build and Install](/docs/db/admin/build) section for the manual build instructions.

## Create Repository and Run Database

A typical workflow consists of the following steps:

{{% steps %}}
1. [Create and Configure Repository](/docs/db/admin/create)
2. [Start server](/docs/db/admin/start_stop)
{{% /steps %}}

By default, the server accepts **`HTTP`** connections on port **`8080`** and the **`UNIX socket file`**
created in the repository.

It is now ready to work.

For security reasons, Amelie will listen only on the **`localhost`** addresses. Local connections
considered secure will be allowed to connect as the **`amelie`** superuser without
authentication.

External connections must be [configured manually](/docs/db/admin/create)
and will require to:

{{% steps %}}
1. [Create Users and Agents](/docs/db/admin/auth)
2. [Configure TLS certificates](/docs/db/admin/tls)
{{% /steps %}}

## Connect

After the repository is created and the server started, it is now possible to:

* [Connect](/docs/db/admin/cli) to the server using Console Client
* [Create Users and Agents](/docs/db/admin/auth)
* [Import](/docs/db/admin/import) data from files
* Create your Client Applications using the [API](/docs/api/http) and [SQL](/docs/sql/overview)

## Maintenance

A typical server Maintenance should include:

* [Monitoring](/docs/db/admin/monitoring)
* [Periodic Backups](/docs/db/admin/backup)

Additionally, it is possible to setup [Replication](/docs/sql/system/repl/overview).

---

```sh
# create repository and run the server
amelie init ./repo
amelie start ./repo

# stop running server
amelie stop ./repo

# connect using http
amelie http://localhost

# connect using unixsocket
amelie ./repo
```
