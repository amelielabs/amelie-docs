---
weight: 4
title: "Main"
bookToc: false
---

## Main Settings

| Name              | Type     | Mode      | Description |
| :---------------- | :------: | :----:    | :---- |
| version           |  string  | read-only | Server version |
| uuid              |  string  | cli       | Server ID |
| directory         |  string  | read-only | Base directory |
| timezone_default  |  string  | cli       | Default server timezone |
| timezone          |  string  | session   | Session timezone, set to `timezone_default` if not defined |

---

```SQL
show uuid
["a74fbf39-cc9d-314e-a33e-3aa47559ffe5"]

select system.config().uuid
["a74fbf39-cc9d-314e-a33e-3aa47559ffe5"]
```
