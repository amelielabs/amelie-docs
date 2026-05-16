---
weight: 6
title: Users and Authentication
bookToc: true
---

# Users and Authentication

Local connections considered secure will be allowed to connect as the **`amelie`** superuser
and other users without authentication. Same applies to the connections made by the unix socket.

External connections must be allowed and [configured manually](/docs/db/admin/create).
The server will validate each API request [authentication tokens](/docs/api/http_api) and match existing users.

## Superuser

There are only one superuser in the database called **`amelie`**. The superuser cannot be renamed, altered or being dropped.

It is forbidded to use **`amelie`** superuser in remote connections.

## Users and Agents

The [CREATE USER](/docs/sql/ddl/users/create) or [DROP USER](/docs/sql/ddl/users/drop) commands can be used to add new users or delete existing ones.

Currently the [CREATE AGENT](/docs/sql/ddl/users/create) is identical to [CREATE USER](/docs/sql/ddl/users/create), but will mark
those users as agents in the catalog metadata.

## Authentication

Amelie authentication is based on using **[JSON Web Tokens](https://jwt.io/)**.

The client JWT token can be created using the [CREATE TOKEN](/docs/sql/ddl/users/create_token) command or
any external authentication service. The server is using internal randomly generated secret to sign
and validate server-issued tokens. The secret is not exposed outside and can be rotated to invalidate all issued tokens.

It is possible to [REVOKE TOKEN](/docs/sql/ddl/users/alter) for a user.

---

```SQL
-- create user
CREATE USER example;

-- create user JWT token (signed by the server)
CREATE TOKEN example EXPIRE '3 month';

token
─────
"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiAiZXhhbXBsZSIsICJpYXQiOiAxNzc4OTM1MTM1LCAiZXhwIjogMTc4MTYxMzUzNX0.l0yN5LYcSOPuC56lPfPPG4QswkOJLoWeowSkQJE8l5o"
```
