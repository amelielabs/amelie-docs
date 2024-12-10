---
weight: 1
title: Overview
type: docs
bookToc: false
---

## SQL

The SQL dialect is mostly based on **`PostgreSQL`** and **`Standard SQL`** extended with native JSON support. 

## JSON and HTTP Native

We wanted to create a modern, easy-to-use DBMS that is seamlessly compatible with most programming languages
and tooling over **`HTTP`**.

* The database works over **`HTTP`** and accepts **`plain-text SQL`**
* JSON is used for results by default
* JSON arrays and objects can be constructed without functions using the **`[]`**, **`{}`** operators
* JSON fields can be accessed directly without functions using the **`.`** and **`[`** operators
* JSON columns can store any JSON value (not only object) and is using memory efficient encoding
* Expressions and subqueries can be executed natively inside JSON objects
---
