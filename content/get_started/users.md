---
weight: 2
title: Users and AI Agents
bookToc: true
---

# Users and AI Agents

In Amelie, every user or agent is itself a complete database.

This means you can:


* **Create and Isolate** relations, data and permissions per user/agent naturally
* **Share relations** between users and agents with fine-grained control
* Give each agent its own **private workspace** instantly
* **Enforce policies**, expiration, or CASCADE drop child users and agents.

This model eliminates the need for complex multi-tenancy logic — each user/agent gets its own
fully isolated relational database by default.

Additionally, [Table Cloning](/docs/get_started/cloning) provides a powerful solution for multi-tenancy.

Thousands of users or agents can safely share the same tables, indexes, and partitions while
maintaining strong isolation and independent access control.
