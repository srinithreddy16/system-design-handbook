# DB Constraints

## Chapter 20: Database Constraints

Why constraints? Users come from different backgrounds and may enter wrong or faulty data. Forms validate input, and the database enforces rules through constraints. Bad data is useless data.

### 1. UNIQUE

No two rows can have the same value in that column.

Example: username. If `abc` is taken, nobody else can use it (like Instagram or Gmail suggesting alternatives when a username is taken).

### 2. NOT NULL

The column must have a value. It cannot be empty.

Example: `first_name`. We address users by it, so it's required.

### 3. PRIMARY KEY

The unique identifier for each row in a table.

- No two rows share the same value.
- Searching for `id = 3` returns exactly one record.
- It is also used to link tables together (see foreign key).

### 4. CHECK

Enforces a rule on the value.

Examples:

- Password length must be greater than 8, with a number and a special character
- Phone number must contain digits only
- First name must be at least 2 characters long

### 5. FOREIGN KEY

A column in one table that points to the primary key of another table. It links the two tables.

Example: a blog site

`authors` table:

| id (PK) | first_name |
| --- | --- |
| 1 | Ash |
| 2 | Gaurav |

`posts` table:

| id (PK) | content | author_id (FK) |
| --- | --- | --- |
| 1 | HTML basics | 1 |
| 2 | Intro to AI | 2 |

- `author_id` is a foreign key pointing to `authors.id`.
- Post 1 was written by Ash (ID 1) and post 2 by Gaurav (ID 2).
- We don't repeat the author's details in every post. We just store the ID.

```
authors.id (Primary Key)  <────  posts.author_id (Foreign Key)
```

### 6. DEFAULT

Gives a column a fallback value when none is supplied.

Examples:

- Subscription plan: defaults to `free` if the user hasn't paid
- LMS user role: defaults to `student`, since most users are students. It can later be changed to `trainer` or `admin`.

## Constraints Cheat Sheet

| Constraint | Rule | Example |
| --- | --- | --- |
| UNIQUE | No duplicate values | `username` |
| NOT NULL | Value required | `first_name` |
| PRIMARY KEY | Unique identifier for each row | `id` |
| CHECK | Value must satisfy a condition | phone is digits only |
| FOREIGN KEY | Links to another table's primary key | `posts.author_id` |
| DEFAULT | Auto-fills a value if none is given | `role = 'student'` |

## Sample SQL

```sql
CREATE TABLE authors (
  id          INT PRIMARY KEY,
  first_name  VARCHAR(50) NOT NULL CHECK (LENGTH(first_name) >= 2),
  username    VARCHAR(50) UNIQUE,
  role        VARCHAR(20) DEFAULT 'student'
);

CREATE TABLE posts (
  id         INT PRIMARY KEY,
  content    TEXT NOT NULL,
  author_id  INT,
  FOREIGN KEY (author_id) REFERENCES authors(id)
);
```

## Key Takeaways

- A database stores data permanently, so it survives server restarts.
- SQL stores data in related tables (rows and columns). NoSQL has several other models.
- Table names are plural by convention.
- Constraints protect data quality at the database level.
- Primary key + foreign key is how tables are linked.

The transcript ends as the next relational database topic begins, so these notes cover everything up to that point.
