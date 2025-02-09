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
$ amelie --help
amelie (version: 0.1.0)

usage: amelie [command | login] [options]

  commands:

    init   <path> [server options]
    start  <path> [server options]
    stop   <path>
    backup <path> [login] [client options]
    client [login] [client options]
    import [login] [client options] [options] table files
    top    [login] [client options]
    bench  [login] [client options] [options]
    login  <login> [client options]
    logout <login>

  client options:

    --name=string
    --uri=string
    --user=string
    --secret=string
    --token=string
    --path=string
    --tls_capath=string
    --tls_ca=string
    --tls_cert=string
    --tls_key=string
    --tls_server=string
    --debug=string
    --json=string

  server options:

    --uuid=string
    --timezone=string
    --format=string
    --shutdown=string
    --log_enable=bool
    --log_to_file=bool
    --log_to_stdout=bool
    --log_connections=bool
    --log_options=bool
    --tls_capath=string
    --tls_ca=string
    --tls_cert=string
    --tls_key=string
    --listen=json
    --limit_send=int
    --limit_recv=int
    --limit_write=int
    --frontends=int
    --backends=int
    --wal_size=int
    --wal_sync_on_rotate=bool
    --wal_sync_on_write=bool
    --repl_reconnect_ms=int
    --checkpoint_interval=string
    --checkpoint_workers=int
    --json=string

  bench options:

    --type=string
    --threads=int
    --clients=int
    --time=int
    --scale=int
    --batch=int
    --init=bool
    --unlogged=bool

  import options:

    --format=string
    --clients=int
    --batch=int

```
