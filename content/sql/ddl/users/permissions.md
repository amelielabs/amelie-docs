---
weight: 5
title: "Permissions"
bookToc: true
---

# Permissions and Ownership

Amelie designed with the idea that each user/agent gets a sense that it owns
a fully isolated relational database.

All users/agents have full ownership on their relations.

[GRANT/REVOKE](/docs/sql/ops/grant) allows to share relations with other users or agents or
restrict access to the database.

#### Default user/agent permissions

```text
 CREATE_TOKEN
 CREATE_TABLE
 CREATE_FUNCTION
 CREATE_TOPIC
 CREATE_SUBSCRIPTION
 GRANT
 SQL
 RPC
```

### Objects 

| Name                | Description |
| :----------------   | :---- |
| CREATE_USER         | Permission to create users |
| CREATE_TOKEN        | Permission to create auth tokens |
| CREATE_TABLE        | Permission to create tables |
| CREATE_BRANCH       | Permission to create branches |
| CREATE_FUNCTION     | Permission to create functions |
| CREATE_TOPIC        | Permission to create topics |
| CREATE_SUBSCRIPTION | Permission to create subscriptions |

### Operations

| Name                | Description |
| :----------------   | :---- |
| INSERT              | Permission to INSERT |
| UPDATE              | Permission to UPDATE |
| DELETE              | Permission to DELETE |
| PUBLISH             | Permission to PUBLISH |
| SELECT              | Permission to SELECT |
| EXECUTE             | Permission to EXECUTE |
| GRANT               | Permission to GRANT/REVOKE |
| SYSTEM              | Permission to execute system commands. |


### Connections / API permissions

| Name                | Description |
| :----------------   | :---- |
| SERVICE         | Permission to do replication/backup connections. |
| RPC         | Permission to execute JSON-RPC API. |
| SQL         | Permission to execute SQL commands (including HTTP/JSON-RPC API). |
