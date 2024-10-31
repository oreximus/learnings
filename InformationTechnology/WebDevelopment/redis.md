## Redis Crash Course

### Definition of Redis from the Official Wesbite!

- The open-source, in-memory data store used by millions of
developers as a database, cache, streaming engine, and message
broker.

### What is the proble that Redis Solves?

```mermaid

---
title: Old/Common way to Query Server for User Requested Data
---

stateDiagram-v2
    u1: "User"
    s1: "Server"
    d1: "PostgresDB"
    
    direction LR
    u1 --> s1: Request the Data from the Server
    s1 --> d1: Query the data from the Database

    s1 --> u1: Requested Data will be Delivered with a Response
    d1 --> s1: Fetched Data will get Back to the server
```

- The above process will take place again entirely if we refresh
the page from the user side, again the data will be requested 
from the server and again the server will query the data from 
the database the return back the data!
