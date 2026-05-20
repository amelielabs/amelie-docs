---
weight: 3
title: "Embedded API"
bookToc: true
---

# Embedded API

Amelie can be used as a shared library together with your application.

This allows for maximum performance and lowest latency,
since no network IO will be involved. The embeddable mode has no limitations compared to
standalone server deployment - remote hot backup and replication can be used if necessary.

Amelie **Embedded API**
can be used to write directly to the local repository or act as a client to a remote server. In such
a case, Amelie will handle all HTTP/Auth communications in an optimized way.

It allows async execution of requests, making it easier to integrate into applications' event loops.

All functions are FFI-friendly.

-> **[Amelie Embedded API header](https://github.com/amelielabs/amelie/blob/main/amelie/system/api/amelie.h)**

-> **[Amelie Embedded API usage examples](https://github.com/amelielabs/amelie/tree/main/misc/examples)**

```text
AMELIE_API amelie_t*
amelie_init(void);

AMELIE_API void
amelie_free(void*);

AMELIE_API int
amelie_open(amelie_t*, const char* path, int argc, char** argv);

AMELIE_API amelie_session_t*
amelie_connect(amelie_t*, const char* uri);

AMELIE_API amelie_request_t*
amelie_execute(amelie_session_t*, const char* command, int argc, amelie_arg_t*,
               amelie_on_complete_t, void*);

AMELIE_API int
amelie_wait(amelie_request_t*, uint32_t time_ms, amelie_arg_t*);
```
