---
weight: 5
title: "Logger"
bookToc: false
---

## Logger Settings

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----:       | :---- |
| log_enable        |  bool    | cli          | Log messages |
| log_to_file       |  bool    | cli          | Write log messages to file inside the base directory |
| log_to_stdout     |  bool    | cli          | Duplicate log message to stdout |
| log_connections   |  bool    | cli, session | Log connect/diconnect client events |

---

```SQL
show log_connections
[true]
```
