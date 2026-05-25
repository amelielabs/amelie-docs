---
weight: 4
title: CLI
bookToc: true
---

# Console Client

The **`amelie`** command starts a console client using connection options.

The **`amelie bookmark`** command can save and manage server connection options by name.

```text
amelie [path | uri | bookmark_name] [options]
amelie bookmark [options]
```

If the first argument is recognized as a local path, unix socket connection will be initiated.
Otherwise the client will search for a bookmark by name or URI.

The client uses the **`AMELIE_HOME`** environment variable to identify its home directory. If the variable is not
provided, it will use **`~/.amelie`**. The home directory contains a bookmark information file and a history file.

The following connection options are supported:

| Argument             | Type | Description |
| :----------------    |  :----:  | :----      |
|  uri             | string | Remote server URI (uri or path is mandatory).|
|  path            | string | Unix socket path. |
|  user            | string | User name (**amelie** is default). Can override URI user name. |
|  token           | string | Client authentication token.
|  timezone        | string | Client timezone.
|  tls_capath      | string | TLS CA directory path. |
|  tls_ca          | string | TLS CA certificate file path. |
|  tls_cert        | string | TLS Client certificate file path. |
|  tls_key         | string | TLS Client certificate private key file path. |
|  tls_server      | string | TLS Server option. |

## Execute SQL commands from Pipe

The client can be run in a pipe mode to execute **`SQL`** commands from **`stdin`**.

```sh
cat file.sql | amelie http://localhost
```

While reading commands in the pipe mode the client will separate input statements using the **`;`** symbol and send each of
them separately.

If the input starts with **`BEGIN`**, the client will read statements until the closing **`END`**
statement and only then send the transaction for execution. Same logic applies to the control structures.

---

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

```sh
# connect to the server using the unix socket
amelie ./repo

# connect to the server without authentication as amelie superuser
amelie http://localhost

# connect to the server as test user
amelie http://test@localhost

# connect to the server as test user with authentication token
amelie http://test@localhost --token="..."

# connect to the server using bookmark
amelie bookmark home http://test@localhost --token="..."
amelie home

# connect to the server and send SQL commands for execution
cat file.sql | amelie home

# remove the `home` bookmark
amelie bookmark home
```
