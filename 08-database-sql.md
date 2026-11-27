# Relational Database - SQL

## Chapter 19: Relational Database (SQL)

SQL = Structured Query Language. It belongs to the family of relational databases.

### Core idea

- Data is stored in tables.
- Each table is roughly one entity: users, posts, comments, videos, etc.
- Tables can be related to each other.

### Anatomy of a table

Example `users` table:

| id | first_name | last_name | phone |
| --- | --- | --- | --- |
| 1 | Ash | Agarwal | 9876543210 |
| 2 | Gaurav | Sharma | 9123456780 |

| Term | Meaning | In the example |
| --- | --- | --- |
| Table | A collection of one kind of entity | `users` |
| Column (attribute) | One property of the entity | `first_name` |
| Row (record) | One complete entry | The row for Ash |

### Naming convention

Use plural table names: `users`, `posts`, `comments`, `videos`.

This is a convention rather than a strict rule, but it makes sense because one table holds many records.
