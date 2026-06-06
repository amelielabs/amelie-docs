---
weight: 2
title: "JSON-RPC / Websocket API"
bookToc: true
---

# JSON-RPC API

Amelie **JSON-RPC API** follows the [JSON-RPC 2.0 Specification](https://www.jsonrpc.org/specification).

### Request

Request body has the following structure:

```json
{
  "jsonrpc": "2.0",
  "id": <value>,
  "method": "<method_name>",
  "params": <value>
}
```

The **id** field will be returned in the reply as is and can be used by the
client to identify the request.

The **params** field depends on the **method** being used.

### Reply

```json
{
  "jsonrpc": "2.0",
  "id": <value_from_request>,
  "result": <value>
}
```

The **result** depends on the method. Query result format matches the [HTTP API](/docs/api/http):

```json
{"columns": [...], "rows": [[...], ...]}
```

#### Reply format for real-time events

```json
{
  "jsonrpc": "2.0",
  "method": "event",
  "params": {
    "lsn": <value>,
    "lsn_op": <value>,
    "cmd": "<name>",
    "user": "<user_name>",
    "name": "<relation_name>",
    "row": <value>
  }
}
```

For real-time streaming notifications the **id** field would be missing.

### Methods

Following methods are supported:

### SQL

```json
{
  "jsonrpc": "2.0",
  "id": <value>,
  "method": "sql",
  "params": {
    "text": "<SQL text>"
  }
}
```

Execute plain text SQL command.

### Write

```json
{
  "jsonrpc": "2.0",
  "id": <value>,
  "method": "write",
  "params": {
    "user": "<user_name>",
    "name": "<relation_name>",
    "arguments": [{...}, ...]
  }
}
```

Generic write method that can do single argument or batch **insert**, **execute function**, or
**publish** based on the target relation.

Each argument object key/values must match relation columns names and types.

**user** field is optional.

### Ack

```json
{
  "jsonrpc": "2.0",
  "id": <value>,
  "method": "ack",
  "params": {
    "user": "<user_name>",
    "name": "<relation_name>",
    "arguments": [lsn, lsn_op]
  }
}
```

Acknowledge subscription.

**user** field is optional.

### Follow

```json
{
  "jsonrpc": "2.0",
  "id": <value>,
  "method": "follow",
  "params": {
    "user": "<user_name>",
    "name": "<relation_name>"
  }
}
```

Start real-time streaming of relation updates.
This command is available only when using **`websocket`** connection.

The relation can be a **subscription**, **table**, **table clone** or **topic**.
It is possible be subscribed on multiple relations.

**user** field is optional.

Client will start receiving real-time update events.

### Unfollow

```json
{
  "jsonrpc": "2.0",
  "id": <value>,
  "method": "unfollow",
  "params": {
    "name": "<relation_name>"
  }
}
```

Stop real-time streaming.

---

```text
wscat -c http://localhost:8080/rpc

> {"jsonrpc": "2.0", "id": 0, "method": "follow", "params": {"name": "x"}}
< {"jsonrpc": "2.0", "id": 0, "result": {}}
>  {"jsonrpc": "2.0", "id": 0, "method": "write", "params": {"name": "x", "arguments": [1,2,3]}}
< {"jsonrpc": "2.0", "id": 0, "result": {}}
{"jsonrpc": "2.0", "method": "event", "params": {"lsn": 9, "lsn_op": 0, "cmd": "publish", "user": "amelie", "name": "x", "row": 1}}
{"jsonrpc": "2.0", "method": "event", "params": {"lsn": 9, "lsn_op": 1, "cmd": "publish", "user": "amelie", "name": "x", "row": 2}}
{"jsonrpc": "2.0", "method": "event", "params": {"lsn": 9, "lsn_op": 2, "cmd": "publish", "user": "amelie", "name": "x", "row": 3}}

```
