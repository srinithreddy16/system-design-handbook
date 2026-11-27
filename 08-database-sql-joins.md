# DB Joins

Chapters 21, 22 and 23. How tables relate to each other in SQL, why NoSQL exists, when to pick which, and the four NoSQL types.

## Chapter 21: Database Joins (Relationships)

A join connects two tables so we can manage relationships between entities. There are four relationship types.

### 1. One-to-Many

One record in table A relates to many records in table B.

Example: one author writes many blogs.

`users`

| id | fname |
| --- | --- |
| 1 | Ash |
| 2 | Gaurav |

`blogs`

| id | content | author_id |
| --- | --- | --- |
| 1 | HTML | 1 |
| 2 | AI | 2 |
| 3 | System Design | 1 |

Ash (ID 1) has two blogs. The foreign key `author_id` stores the link.

### 2. Many-to-One

The same relationship seen from the other side: many blogs belong to one user.

One-to-many and many-to-one are the same relationship, just viewed from different tables.

### 3. Many-to-Many

Many records in A relate to many records in B, and vice versa.

Example: students and courses.

- A student can enroll in many courses.
- A course can have many students.

This needs a junction table (also called a join or bridge table) in between.

`students`

| id | fname |
| --- | --- |
| 1 | Ash |
| 2 | Gaurav |

`courses`

| id | name |
| --- | --- |
| 1 | Master Java |
| 2 | Master AI |

`students_courses` (junction table)

| id | student_id | course_id |
| --- | --- | --- |
| 1 | 1 | 1 |
| 2 | 1 | 2 |
| 3 | 2 | 1 |
| 4 | 2 | 2 |

Each row means "this student is enrolled in this course." Now we can see how many courses a student has and how many students a course has.

```
students ──< students_courses >── courses
```

### 4. One-to-One

One record in table A relates to exactly one record in table B.

Example: a platform with text blogs, audio podcasts, and videos.

Approach A: one big table. A single `contents` table with a `type` column (text, audio, video).

Problem: each type is processed very differently, so the table gets heavy, and filtering becomes slow.

Approach B: split it up.

- A light `contents` table holds only searchable details: id, name, type, keywords, slug.
- The actual data lives in separate tables: `blogs`, `audios`, `videos`.
- The type tells you which table to look in.

`contents`

| id | name | type |
| --- | --- | --- |
| 1 | System Design | video |

→ go to `videos` where `id = 1`.

Each content row maps to exactly one row in one specific table. That is a one-to-one relationship.

## Joins Summary

| Relationship | Meaning | Example |
| --- | --- | --- |
| One-to-Many | 1 row ↔ many rows | Author → blogs |
| Many-to-One | Many rows ↔ 1 row | Blogs → author |
| Many-to-Many | Many ↔ many (needs a junction table) | Students ↔ courses |
| One-to-One | 1 row ↔ exactly 1 row | Content → its video |
