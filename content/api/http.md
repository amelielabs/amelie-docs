---
weight: 1
title: "HTTP API"
bookToc: true
---

# HTTP API

<style>

.api {
  margin-bottom: 60px;
}

.api_header {
  font-size: 18px;
  font-family: monospace;
  font-weight: 300;

  padding: 15px;
  border-radius: 10px;
  background: #f0f0f0;
}

</style>

<div class="api">
<div class="api_header">
POST /sql (text/plain)
</div>

| Header            | Optional | Description |
| :-----------      | :----    | :---- |
| Content-Type  | Yes | text/plain (default) |
| Accept       | Yes | text/plain or application/json (default) |
| X-User-Id     | Yes | user name (**amelie** by default) |
| Authorization | Yes | JWT token |

Simple endpoint to work with plain-text SQL for Console and Human interactions or other
sentient beings. Output either
plain text (rendered on the server) or JSON.

</div>

<div class="api">
<div class="api_header">
POST /rpc (application/json)
</div>

| Header            | Optional | Description |
| :-----------      | :----    | :---- |
| Content-Type  | Yes | appliation/json (default) |
| Accept        | Yes | application/json (default) |
| X-User-Id     | Yes | user name (**amelie** by default) |
| Authorization | Yes | JWT token |

[JSON-RPC API](/docs/api/jsonrpc) endpoint. 

General use endpoint for applications and agents. Accept and reply only JSON according to
the protocol API.
</div>

<div class="api">
<div class="api_header">
GET /rpc (application/json) websocket
</div>

| Header            | Optional | Description |
| :-----------      | :----    | :---- |
| Content-Type  | Yes | appliation/json (default) |
| Accept        | Yes | application/json (default) |
| X-User-Id     | Yes | user name (**amelie** by default) |
| Authorization | Yes | JWT token |

[JSON-RPC API](/docs/api/jsonrpc) over Websockets. 

General use endpoint for applications and agents. Accept and reply only JSON according to
the protocol API.

Supports [Real-Time Streaming](/docs/get_started/streaming).

The request headers must additionally include common websocket
protocol upgrade headers.

</div>

### Authentication

Amelie authentication is based on using **[JSON Web Tokens](https://jwt.io/)**. Authentication is mandatory
for all non-local connections.

If authentication is used, the incoming HTTP request header must include the **`Authorization`** field with
a valid JWT token in the format:

```text
Authentication: Bearer <JWT>
```

The client JWT token can be created using the [CREATE TOKEN](/docs/sql/ddl/users/create_token) command.

### Responses

| Status code       | Description |
| :---------------- | :---- |
| 200 OK            | OK |
| 204 No Content    | OK with empty reply |
| 400 Bad Request       | Invalid URI or execution error |
| 403 Forbidden         | Authentication or access error |
| 413 Payload Too Large | Limits reached |

Example of the json result format for the **/sql** endpoint:

```json
{"columns": [...], "rows": [[...], ...]}
```
Example of the json error format for the **/sql** endpoint:

```json
{"msg": "..."}
```

---

```text
curl -X POST http://localhost:8080/sql \
  -H "Accept: text/plain" \
  -d "SELECT 1 as one, 2 as two"

one  two
──────────
1    2
```

```text
curl -X POST http://localhost:8080/sql \
  -d "SELECT 1 as one, 2 as two" \
{"columns": ["one", "two"], "rows": [[1, 2]]}
```
