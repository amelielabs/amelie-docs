---
weight: 5
title: "Import JSONL data"
bookToc: false
---

## Import JSON Lines data

### **`POST /schema/table (application/jsonl)`**

Insert one or more rows to the **`table`** using the [JSON Lines](https://jsonlines.org/) format inside a single transaction.
The **`POST`** path must include the table **`schema`** and the **`table`** name.

Each row must start with either an **`array`** or an **`object`**. The **`object`** will be accepted only if the
table has one [OBJECT](/docs/sql/types/object) column or the provided column list has one column.

Providing the optional **`columns`** argument in the query, it is possible to pass the column list:
**`POST /schema/table&columns=a,b`**. If the column list is provided, each row will be interpreted accordingly.
The column list follows the logic described by the [INSERT](/docs/sql/dml/insert) command.

The [import](/docs/tutorial/import) command can be used to import **`JSONL`** data from a file.

---

```http
POST /public/test HTTP/1.1
Content-Type: application/jsonl
Content-Length: 32

[0,0,0]
[1,0,0]
[2,0,0]
[3,0,0]
```

```http
POST /public/test HTTP/1.1
Content-Type: application/jsonl
Content-Length: 40

{"id": 0}
{"id": 1}
{"id": 2}
{"id": 3}
```

```sh
curl -X POST \
-H "Content-Type: application/jsonl" \
--data-binary "@file.jsonl" \
"http://localhost:3485/public/test"
```

```sh
# import JSONL file data to the test table
amelie import --uri="localhost" test file.jsonl

# import compressed JSONL file to the test table
zcat file.jsonl.gz | amelie import home --format=jsonl test
```
