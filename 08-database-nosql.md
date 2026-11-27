# Non-Relational Database - NoSQL

## Chapter 22: NoSQL (Non-Relational Databases)

### The problem with SQL for growing apps

Take a simple blog with posts and comments. In SQL we may need:

`posts`, `images`, `videos`, `text`, `contents`, `comments`, `users`

That is 6 or more tables, plus relationships between all of them. As the app grows, this becomes hard to scale.

### How databases scale

| Type | What it means | Limit |
| --- | --- | --- |
| Vertical | Add more capacity to one server | Hits a ceiling |
| Horizontal | Spread data across many servers | Works, but relationships across servers are hard to maintain in SQL |

### Advantages of NoSQL

#### 1. Easy to scale

Each record is a self-contained document, so it can be replicated across servers or partitioned (split) across servers easily.

#### 2. Schemaless (flexible structure)

SQL tables have fixed columns. NoSQL documents can have different fields.

```json
{ "userId": 1, "content": "https://site.com/photo.jpg" }

{ "userId": 2, "content": "Some text here" }

{ "userId": 3, "heading": "Java", "description": "Intro to Java" }
```

Three documents in the same collection, each with different fields. This is impossible in a normal SQL table.

#### 3. Few or no relationships needed

Each entity stands on its own. Nested data lives inside the document.

```json
{
  "courseId": 1,
  "name": "Master Java",
  "lessons": [
    {
      "title": "Intro",
      "comments": [ { "user": "Ash", "text": "Great!" } ]
    }
  ]
}
```

In SQL, this would need separate `courses`, `lessons`, and `comments` tables plus joins.

#### 4. Faster reads

Everything is in one document, so there is no need to traverse and join many tables.

### Who uses NoSQL?

| Company | Database | Used for |
| --- | --- | --- |
| Netflix | Apache Cassandra | User activity |
| Amazon | DynamoDB | Scaling the application |
| Facebook / Meta | HBase | Messaging and large-scale storage |
| Uber | MongoDB | Flexible, real-time data |
| Twitter / X | Redis | Caching and timelines |

### SQL vs NoSQL: When to Pick Which

| Pick SQL when | Pick NoSQL when |
| --- | --- |
| Consistency is the top priority | Availability and scalability matter more than strict consistency |
| Payments and transactions | Huge scale and high speed |
| Schema is fixed | Schema changes or is unstructured |
| Relationships must be handled perfectly | Few relationships between data |

Rule of thumb: consistency first → SQL. Availability and scale first → NoSQL.
