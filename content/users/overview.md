---
weight: 1
title: "Overview"
bookToc: false
---

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
