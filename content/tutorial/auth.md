---
weight: 6
title: Authentication and Users
bookToc: false
---

## Authentication and Users

By default, the Server runs without authentication and accepts **`HTTP`** connections on the **`3485`** port.
The Server will validate each request and match existing users if authentication is enabled.

Learn more about the [User Management and Authentication Tokens](/docs/users/overview).

To enable authentication, the following steps should be done:

1) Create one or more Users
2) Create Authentication Tokens
3) Enable authentication

## Create Users

The [CREATE USER](/docs/users/create) or [DROP USER](/docs/users/drop) commands can be used to add new users or delete existing ones.

Each user must have a valid **`SECRET`** set.

## Create Authentication Tokens

Amelie authentication is based on using **`JSON Web Tokens`** ([JWT](https://jwt.io/)).

The incoming HTTP request header must include the **`Authorization`** field with a valid JWT authentication token.
The client JWT token can be created using the [CREATE TOKEN](/docs/users/create_token) command, manually
using the [jwt()](/docs/sql/functions/crypto) function or any external authentication service. Users secrets are used to sign the tokens.

For security reasons, JWT-based authentication must be used only with **`HTTPS`** connections.

```SQL
create user test secret 'test'

create token test expire '3 month'
["eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiAidGVzdCIsICJpYXQiOiAxNzI3OTYyMzU3LCAiZXhwIjogMTczNTkxMTE1N30.79g-77QHd82f7cSbeZSXaz4lP_7F3J4bm7EuZOUCmmM"]
```

## Enable Authentication

The authentication can be enabled for each listening address individually. For example, it is possible to turn off the
authentication for **`localhost`** and enable for other network interfaces.

Additionally, the Server always creates a Unix socket inside each repository, which can be used to connect to the
database directly without authentication.

To enable the authentication, set **`auth`** to **true** for each desired listen address in the
configuration file:

```SQL
[{
  "host": "*",
  "port": 3485,
  "auth": true
}]
```

Learn more about the [Server Configuration](/docs/configuration/server).
