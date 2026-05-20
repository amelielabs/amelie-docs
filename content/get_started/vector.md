---
weight: 7
title: Vector Search
bookToc: true
---

# Vector Search

Amelie has native vector support built directly into the database, allowing you to perform
fast similarity searches alongside regular OLTP operations.

Thanks to Amelie’s architecture, vector search is **fully parallelized across all CPU cores** and benefits
from SIMD instructions, making it significantly faster than traditional approaches.

```SQL
SELECT
   id, title,
   embedding::cos_distance(vector [..query embedding..])
FROM
   documents
ORDER BY 3 DESC
LIMIT 5;
```

### Use Cases

* **AI Agent Memory** — Store conversation history or knowledge as embeddings and retrieve relevant context
* **Semantic Search** — Power intelligent search in documentation, support tickets, or product catalogs
* **Recommendation Systems** — Find similar users, products, or content
* **RAG (Retrieval-Augmented Generation)** — Retrieve relevant documents for LLMs in real time

Vector search in Amelie works seamlessly with transactions, branching, and real-time subscriptions, making
it ideal for building modern AI-powered applications.
