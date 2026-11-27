# Types of NoSQL Databases

## Chapter 23: Types of NoSQL Databases

"NoSQL" is like saying "not Java." It's a whole family of options. There are four main types.

### 1. Key-Value Store

Data is stored as key → value pairs.

- Key: must be unique.
- Value: can be anything: string, number, JSON, blob, byte array, list, nested object.
- No schema, no relationships.

```
"post:1" → {
  "postId": 1,
  "content": "Hello world",
  "comments": [
    { "commentId": 1, "text": "Nice!" },
    { "commentId": 2, "text": "Thanks" }
  ]
}
```

You already use this idea in: caches, cookies, local storage.

Examples: Redis, DynamoDB.

### 2. Columnar (Column-Oriented) Database

Data is read column by column instead of row by row.

The problem with row-based reading: To find the average marks of a class, a SQL database reads every row left to right, even though we only need the marks column. With 17 columns, that is a lot of wasted reading.

| id | name | marks |
| --- | --- | --- |
| 1 | Ash | 90 |
| 2 | Gaurav | 95 |

Columnar DB: reads only the `marks` column, then sums and averages it. Columns are linked by the common `id`.

| | Columnar DB |
| --- | --- |
| Reads (analytics) | Very fast |
| Writes | Slower (must write column by column) |
| Best for | Analysis and aggregation over huge data |

Examples: Google BigQuery, Amazon Redshift, Databricks.

### 3. Graph Database

Data is stored as nodes (entities) connected by edges (relationships). Think of a detective's board with photos joined by string.

```
(Student) ──enrolled──> (Course)
(Student) ──studies in──> (College) ──provides──> (Course)
```

What makes it special: both nodes and edges can have properties.

- Node: Student `{ name: "Ash" }`
- Edge: enrolled `{ year: 2024, marks: 90 }`

| | Graph DB |
| --- | --- |
| Best for | Finding patterns and connections, analyzing customer behavior |
| Used by | Data scientists, large companies |
| Downside | Can be slower, since there are many entities and relationships with properties |
| Query languages | Gremlin, SPARQL, Cypher |

Example: Neo4j.

### 4. Document Database

Stores documents (JSON-like) of any length. The most popular NoSQL type.

- Schemaless and flexible
- No relationships needed
- Fast retrieval

Common uses:

- Logging: log structures vary (errors, warnings, info)
- User profiles: some users fill many fields, others few
- Content: images, videos, and text posts can all live in one collection with different attributes

Examples: MongoDB, CouchDB.

## NoSQL Types at a Glance

| Type | Stores data as | Best for | Examples |
| --- | --- | --- | --- |
| Key-Value | Key → value pairs | Caching, sessions, simple lookups | Redis, DynamoDB |
| Columnar | Columns | Analytics and aggregation | BigQuery, Redshift |
| Graph | Nodes + edges (with properties) | Relationships and pattern finding | Neo4j |
| Document | JSON-like documents | Flexible, varied data (logs, profiles, content) | MongoDB, CouchDB |

## Key Takeaways

- Joins link SQL tables: one-to-many, many-to-one, many-to-many (junction table), and one-to-one.
- SQL is best for strict consistency, fixed structure, and payments.
- NoSQL is best for scale, speed, flexible structure, and few relationships.
- NoSQL has 4 types: key-value, columnar, graph, and document.
- Real systems often use both SQL and NoSQL for different parts.

The transcript ends as the next topic begins, so these notes cover everything up to that point.
