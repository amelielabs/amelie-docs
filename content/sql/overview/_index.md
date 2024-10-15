---
weight: 1
title: Overview
type: docs
bookToc: false
---

## SQL

The SQL dialect is based on **`PostgreSQL`** and **`traditional SQL`** extended with rich document support. 
We wanted to create an easy-to-use DBMS seamlessly compatible with most programming
languages and tooling over **`HTTP`**.

## JSON and HTTP Native

The whole world speaks JSON, and almost all network services and system interactions are based on it.
However, its support for relation databases is archaic and cumbersome. Moreover, a typical DBMS has a
custom protocol with data types that require client libraries and ORM frameworks.

We designed Amelie as a modern document SQL database to address those issues directly on different levels:

* The database works over **`HTTP`** and accepts **`plain-text SQL`**
* JSON is used for results
* All data types are compatible with JSON and traditional relational types
* All data types can be nested inside a document
* Tables rows are stored as **`memory-efficient JSON`** arrays
* Tables can have a multiple or single JSON column (nested **`PRIMARY KEY`**)
* Objects can be constructed without functions using the **`[]`**, **`{}`** operators
* JSON fields can be accessed directly without functions using the **`.`** and **`[`** operators
* Expressions and subqueries can be executed natively inside JSON objects
* JSON can be part of **`SELECT FROM`** or **`JOIN`** operation
* JSON objects can be used for **`CREATE INDEX`** (nested key)

---
