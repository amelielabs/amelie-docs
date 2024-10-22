---
weight: 5
title: Import Data
bookToc: false
---

## Import Data Files

The **`amelie import`** command can be used to import files into the remote table.

```text
amelie import [login] [client options] [import options] [schema.]table [files]
```


The command is compatible with the [Console Client](/docs/tutorial/cli) options.

The following import options are supported:

| Argument          | Type | Description |
| :---------------- |  :----:  | :----      |
| format        | string | File format to use: **`auto`** (default), **`csv`**, **`jsonl`**. |
| clients       | int | Total number of clients (default is 12). |
| batch         | int | Number of rows in one operation (default is 500). |

The **`table name`** is mandatory and may include the optional **`schema`** name prefix. If the
schema is not provided, it will be set to **`public`**.

If the **`format`** argument is **`auto`**, it will try to guess the format
based on file extensions.

If **`files`** are not provided, the **`stdin`** will be used instead.

---

```sh
# import CSV files to the test table
amelie import --uri="localhost" test *.csv

# import compressed JSON lines file to the test table
zcat file.jsonl.gz | amelie import home --format=jsonl test

# execute SQL commands from file
cat file.sql | amelie home
```
