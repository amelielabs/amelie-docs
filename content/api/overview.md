---
weight: 1
title: "Overview"
bookToc: true
---

## HTTP Request

Currently, the Server supports only **`HTTP/1.1`** **`POST`** operations to
execute **`SQL`** commands and import data based on the **`Content-Type`**.

### Authentication

Amelie authentication is based on using **`JSON Web Tokens`** ([JWT](https://jwt.io/)).

If authentication is enabled, the incoming HTTP request header must include the **`Authorization`** field with
a valid JWT token in the format: **`Authentication: Bearer <JWT>`**.

JWT-based authentication must be used only with **`HTTPS`** connections.

Learn more about [Authentication and Users](/docs/tutorial/auth).

## Authentication and User Management

Amelie authentication is based on using JSON Web Tokens ([JWT](https://jwt.io/)).

If authentication is enabled, the incoming HTTP request header must include the **`Authorization`** field with
a valid JWT token in the format: **`Authentication: Bearer <JWT>`**.

The JWT payload must include a **`sub`** field that identifies a user and **`iat`**, **`exp`** fields. The token must be signed using the
user's secret. Currently, Amelie supports tokens created with the **`HS256`** algorithm.
The client JWT token can be created using the [CREATE TOKEN](/docs/users/create_token) command, manually using
the [jwt()](/docs/sql/functions/crypto) function or any external authentication service.

Amelie will validate each request and match existing users accordingly. The [CREATE USER](/docs/users/create) or
[DROP USER](/docs/users/drop) commands can be used to add new users or delete existing ones.

JWT-based authentication must be used only with **`HTTPS`** connections.

---

```sh
curl -X POST \
     -H "Authorization: Bearer <JWT>" \
     -H "Content-Type: text/plain" \
     -d 'SELECT "hello, world!"' \
     --cacert ca.crt \
     https://localhost:3485/v1/execute
["hello, world!"]
```

---

## HTTP Reply

The Server respond **`Content-Type`** depends on the [FORMAT](/docs/sql/query/format) variable and clause.

Currently, the supported content type is **`application/json`**.

Based on the request result, the Server responds with the following status codes:

### **`200 OK`**

On successful execution, the Server will respond with status code **`200`**, containing a
JSON array with zero or more values:

```http
HTTP/1.1 200 OK
Content-Length: 17
Content-Type: application/json

["hello, world!"]
```

---

### **`204 No Content`**

On successful execution, the Server will respond with status code **`204`** if the result does not have data.

```http
HTTP/1.1 204 No Content
```

---

### **`400 Bad Request`**

In case of an error, the server will respond with status code **`400`**, containing a single JSON object:

```http
HTTP/1.1 400 Bad Request
Content-Length: 41
Content-Type: application/json

{"msg": "unterminated string"}
```

---

### **`403 Forbidden`**

In case of authentication errors, the server will respond with the status code **`403`** without
data and close the client connection.

```http
HTTP/1.1 403 Forbidden
```

---
