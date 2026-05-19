---
weight: 4
title: "Control Structures"
bookToc: true
---

# Control Structures

Currently Amelie supports following control structures with User-Defined Functions.

### IF/ELSE

```SQL
IF expr THEN
  [block]
[ELSIF expr THEN]
  [block]
[ELSE]
  [block]
END;
```

---

### FOR

```SQL
FOR alias IN from_target DO
  [block]
END;
```

---

### WHILE

```SQL
WHILE expr DO
  [block]
END;
```

---


### BREAK / CONTINUE

```SQL
BREAK;
CONTINUE;
```

---

### RETURN

```SQL
RETURN;
RETURN variable;
RETURN expr;
RETURN statement;
```

---
