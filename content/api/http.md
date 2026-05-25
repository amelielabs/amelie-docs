---
weight: 1
title: "HTTP API"
bookToc: true
---

# HTTP API

Amelie is accessible via two HTTP API endpoints for plain-text SQL and JSON-RPC commands,
and via websockets for [Real-Time Streaming](/docs/get_started/streaming).

## SQL endpoint

```text
POST /sql (text/plain)
```

| Header            | Optional | Description |
| :-----------      | :----    | :---- |
| Content-Type  | Yes | text/plain |
| Accept       | Yes | text/plain (default) or application/json |
| X-User-Id     | Yes | user name (**amelie** by default) |
| Authorization | Yes | JWT token |

Simple endpoint to work with plain-text SQL for Console and Human interactions or other
sentient beings. Output either
plain text (rendered on the server) or JSON:

```sh
curl http://localhost:8080/sql \
  -X POST \
  -d "SELECT 1 as one, 2 as two"

one  two
──────────
1    2
```

```sh
curl http://localhost:8080/sql \
  -X POST \
  -H "Accept: application/json" \
  -d "SELECT 1 as one, 2 as two"
{"columns": ["one", "two"], "rows": [[1, 2]]}
```

## JSON-RPC endpoint

```text
POST /rpc (application/json)
```

| Header            | Optional | Description |
| :-----------      | :----    | :---- |
| Content-Type  | Yes | application/json |
| Accept        | Yes | application/json |
| X-User-Id     | Yes | user name (**amelie** by default) |
| Authorization | Yes | JWT token |

[JSON-RPC API](/docs/api/jsonrpc) endpoint. 

General use endpoint for applications and agents. Accept and reply only JSON according to
the protocol API.

## JSON-RPC endpoint over Websocket

```text
GET /rpc (application/json) websocket
```

| Header            | Optional | Description |
| :-----------      | :----    | :---- |
| Content-Type  | Yes | application/json |
| Accept        | Yes | application/json |
| X-User-Id     | Yes | user name (**amelie** by default) |
| Authorization | Yes | JWT token |

[JSON-RPC API](/docs/api/jsonrpc) over Websockets. 

General use endpoint for applications and agents. Accept and reply only JSON according to
the protocol API.

Supports [Real-Time Streaming](/docs/get_started/streaming).

The request headers must additionally include common websocket
protocol upgrade headers.

## Authentication

Amelie authentication is based on using [JSON Web Tokens](https://jwt.io/). Authentication is mandatory
for all non-local connections.

If authentication is used, the incoming HTTP request header must include the **`Authorization`** field with
a valid JWT token in the format:

```text
Authorization: Bearer <JWT>
```

The client JWT token can be created using the [CREATE TOKEN](/docs/sql/ddl/users/create_token) command.

## Responses

| Status code       | Description |
| :---------------- | :---- |
| 200 OK            | OK |
| 204 No Content    | OK with empty reply |
| 400 Bad Request       | Invalid URI or execution error |
| 403 Forbidden         | Authentication or access error |
| 413 Payload Too Large | Limits reached |

Example of the json error format for the **/sql** endpoint:

```json
{"msg": "..."}
```
