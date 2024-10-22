---
weight: 4
title: CLI
bookToc: false
---

## Console Client

The **`amelie client`** command starts a console client using connection options.

The **`amelie login`** and **`amelie logout`** commands can save and manage remote server connection options by a **`login`**.

```text
amelie [login] [options]
amelie client [login] [options]
amelie login  <login> [options]
amelie logout <login>
```

The client uses the **`AMELIE_HOME`** environment variable to identify its home directory. If the variable is not
provided, it will use **`~/.amelie`**. The home directory contains a login information file and a history file.

The following connection options are supported:

| Argument             | Type | Description |
| :----------------    |  :----:  | :----      |
|  uri             | string | Remote server URI (uri or path is mandatory).|
|  path            | string | Unix socket path. |
|  user            | string | User name (used to generate one-time token). |
|  secret          | string | User secret (used to generated one-time token). |
|  token           | string | Client authentication token (includes user name).
|  tls_capath      | string | TLS CA directory path. |
|  tls_ca          | string | TLS CA certificate file path. |
|  tls_cert        | string | TLS Client certificate file path. |
|  tls_key         | string | TLS Client certificate private key file path. |

### Execute SQL commands from Pipe

The client can be run in a pipe mode to execute **`SQL`** commands from **`stdin`**.

```sh
cat file.sql | amelie --uri="http://localhost:3485"
```

While reading commands in the pipe mode the client will separate input statements using the **`;`** symbol and send each of
them separately. If the input starts with **`BEGIN`**, the client will read statements until the closing **`COMMIT`**
statement and only then send the transaction for execution.

---

```sh
# connect to the server using the repository unix socket
amelie ./repo

# connect to the server using URI without authentication
amelie --uri="localhost"
amelie --uri="http://localhost:3485"

# connect to the server using TLS with authentication token
amelie --uri="https://localhost:3485" --token="eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiAidGVzdCIsICJpYXQiOiAxNzI3OTYyMzU3LCAiZXhwIjogMTczNTkxMTE1N30.79g-77QHd82f7cSbeZSXaz4lP_7F3J4bm7EuZOUCmmM"

# connect to the server using TLS, CLI will generate one-time JWT token each time automatically
amelie --uri="https://localhost:3485" --user="test" --secret="test"

# connect to the server using saved credentials, CLI will generate and save JWT token
amelie login home --uri="https://localhost:3485" --user="test" --secret="test"
amelie home

# connect to the server using saved credentials
amelie login home --uri="https://localhost:3485" --token="eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiAidGVzdCIsICJpYXQiOiAxNzI3OTYyMzU3LCAiZXhwIjogMTczNTkxMTE1N30.79g-77QHd82f7cSbeZSXaz4lP_7F3J4bm7EuZOUCmmM"
amelie home

# connect to the server and send SQL commands for execution
cat file.sql | amelie home

# remove information about the `home` login
amelie logout home
```
