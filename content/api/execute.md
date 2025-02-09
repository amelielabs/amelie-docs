---
weight: 2
title: "Execute SQL"
bookToc: false
---

## Execute SQL commands

### **`POST /v1/execute`**

Execute plain text **`SQL`** commands.

The supported **`Content-Type`** is: **`text/plain`** or **`application/sql`**.

All provided statements will be executed as a single multi-statement transaction,
regardless of whether there were **`BEGIN/COMMIT`** statements.

The console [client](/docs/tutorial/cli) can be used to execute **`SQL`** commands from a file or pipe.

---

```http
POST /v1/execute HTTP/1.1
Content-Type: text/plain
Content-Length: 22

SELECT "hello, world!"
```

```sh
# Execute SQL command without authentication
curl -X POST \
     -H "Content-Type: text/plain" \
     -d 'SELECT "hello, world!"' \
     http://localhost:3485/v1/execute
["hello, world!"]
```

```sh
# Execute SQL command with authentication and TLS
curl -X POST \
     -H "Authorization: Bearer <JWT>" \
     -H "Content-Type: text/plain" \
     -d 'SELECT "hello, world!"' \
     --cacert ca.crt \
     https://localhost:3485/v1/execute
["hello, world!"]
```

```sh
# connect to the server using saved credentials, CLI will generate and save JWT token
amelie login home --uri="https://localhost:3485" --user="test" --secret="test"
amelie home

# connect to the server and send SQL commands for execution
cat file.sql | amelie home
```
