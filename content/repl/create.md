---
weight: 2
title: "CREATE REPLICA"
bookToc: false
---

## CREATE REPLICA Statement

```SQL
CREATE REPLICA [IF NOT EXISTS] id [option value ...]
```

Define a new replica by UUID unless it exists. The replica ID must match the replica server instance ID.

Supported options are:

| Argument             | Type | Description |
| :----------------    |  :----:  | :----      |
|  uri             | string | Replica URI (mandatory). |
|  token           | string | Authentication token.  |
|  tls_capath      | string | The CA directory path. |
|  tls_ca          | string | The CA certificate. |
|  tls_cert        | string | The client certificate. |
|  tls_key         | string | The client certificate key. |

Replica connection will start automatically if the replication is active.

---

```SQL
-- set primary id on replica server and start the replication
subscribe "00000000-0000-0000-0000-000000000000";
start repl;

show repl;
[{
  "active": true,
  "role": "replica",
  "primary": "00000000-0000-0000-0000-000000000000"
}]

-- create new replica on the primary server, set replica id and its uri, start replication
create replica "00000000-0000-0000-0000-000000000001" uri "127.0.0.1:3481";
start repl;

show repl;
[{
  "active": true,
  "role": "primary",
  "primary": null
}]
```
