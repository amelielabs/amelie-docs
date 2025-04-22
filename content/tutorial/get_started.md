---
weight: 1
title: Get Started
bookToc: false
---

## Get Started

Amelie is distributed as a single executable file. It provides the functionality of the **Server**,
**Console Client**, and **Benchmark** tool.

Please look at the [Build and Install](/docs/tutorial/build) section for the manual build instructions.

### Usage

A typical workflow consists of the following steps:

1) [Create and Configure Repository](/docs/tutorial/create)
2) [Start server](/docs/tutorial/start_stop)

By default, the Server runs without authentication and accepts **`HTTP`** connections on the **`3485`** port and a
**`UNIX socket file`** in the directory.

After the repository is created and the Server started, it is now possible to:

1) [Connect](/docs/tutorial/cli) to the Server using Console Client
2) Do [Benchmarking](/docs/tutorial/benchmark) and [Monitor](/docs/tutorial/monitoring) the performance
3) [Import](/docs/tutorial/import) data from files
4) Create your Client Applications using the [HTTP API](/docs/api/overview) and [SQL](/docs/sql/overview)

To make the Server secure, it would additionally require to:

1) [Create Users](/docs/tutorial/auth)
2) [Create Authentication Tokens](/docs/tutorial/auth)
3) [Enable Authentication](/docs/tutorial/auth)
4) [Configure TLS Certificates](/docs/tutorial/tls)

A Typical Server Maintenance should include:

1) [Monitoring](/docs/tutorial/monitoring)
2) [Periodic Backups](/docs/tutorial/backup)

Additionally, it is possible to setup [Replication](/docs/repl/overview).

---

```text
amelie (version: 0.3.0)

Usage: amelie [COMMAND | LOGIN] [OPTIONS]

Commands:

  init       Create a database repository
  start      Start a server
  stop       Stop a server
  backup     Create backup of a remote server
  login      Create or update login information
  logout     Delete login information
  client     Connect to a remote server
  import     Import data to a remote server
  top        Get information about remote server
  bench      Run benchmarks on a server
  test       Run tests
```
