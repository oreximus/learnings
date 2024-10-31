## Redis Crash Course

### Definition of Redis from the Official Wesbite!

- The open-source, in-memory data store used by millions of
developers as a database, cache, streaming engine, and message
broker.

### What is the proble that Redis Solves?

```mermaid

---
title: Old/Common way to Query Server for User Request Data
---

stateDiagram
    diagram LR
    U['User'] -- "Request for Data" --> S['Server']
    S -- "Querying Data from the Database" --> D['PostgresDB']
```
