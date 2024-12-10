---
weight: 3
title: "Import CSV data"
bookToc: false
---

## Import CSV data

### **`POST /schema/table (text/csv)`**

Insert one or more rows to the **`table`** using the **`CSV`** format inside a single transaction.
The **`POST`** path must include the table **`schema`** and the **`table`** name.

Providing the optional **`columns`** argument in the query, it is possible to pass the column list:
**`POST /schema/table?columns=a,b`**. If the column list is provided, each row will be interpreted accordingly.
The column list follows the logic described by the [INSERT](/docs/sql/dml/insert) command.

The [import](/docs/tutorial/import) command can be used to import **`CSV`** data from a file.

---

```http
POST /public/test HTTP/1.1
Content-Type: text/csv
Content-Length: 24

1,0,0,0
2,0,0,0
3,0,0,0
```

```sh
curl -X POST \
-H "Content-Type: text/csv" \
--data-binary "@file.csv" \
"http://localhost:3485/public/test"
```

```sh
# import CSV files to the test table
amelie import --uri="localhost" test *.csv

# import compressed CSV file to the test table
zcat file.csv.gz | amelie import home --format=csv test
```
