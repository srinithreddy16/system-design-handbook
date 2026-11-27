# Database

Chapters 18, 19 and 20. Why we need databases, how relational (SQL) databases store data, and the constraints that keep that data correct.

## Chapter 18: Why Do We Need a Database?

A basic application has a client (web or mobile) talking to a server.

If the server alone holds the data, everything is lost when the server restarts. We need somewhere to store data permanently, so that users find it the next time they log in. That place is the database.

Almost every application depends on a database.

### Two approaches: SQL and NoSQL

| | SQL | NoSQL |
| --- | --- | --- |
| Type | Relational database (RDBMS) | Non-relational |
| How data is stored | Tables with rows and columns, linked using joins | Several different models (see below) |
| Examples | PostgreSQL, MySQL | MongoDB, Cassandra |

NoSQL is not one thing. Saying "NoSQL" is like saying "Not Java": it covers many options:

| NoSQL model | Stores data as | Example |
| --- | --- | --- |
| Key-value | Key and value pairs | Redis |
| Document | JSON-like documents | MongoDB |
| Column | Column families | Cassandra |
| Graph | Nodes and relationships | Neo4j |

Your choice of SQL or NoSQL becomes the foundation of how your data is stored. This chapter covers SQL. NoSQL comes next.
