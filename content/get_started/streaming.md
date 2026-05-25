---
weight: 6
title: Real-Time Streaming
bookToc: true
---

# Real-Time Streaming

Amelie provides real-time capabilities through **[JSON-RPC API](/docs/api/jsonrpc)** over WebSockets.

You can execute normal commands (execute sql, insert, publish, call functions, etc.) and subscribe to changes
in the same connection using the **follow** command.

You can follow:

* Any table
* Any table clone
* Any topic
* Any existing subscription

### How it works

* Changes are pushed to you in real-time as they occur
* You can run regular commands and receive subscription events in the same WebSocket session in real-time
* **Follow** on multiple relations
* Use **unfollow** to stop receiving updates

This makes Amelie ideal for building live dashboards, real-time agent coordination, notification systems,
and any application that needs instant updates.
