# RESTful Request

REST is the most widely used API style in the world. This chapter covers JSON, endpoints, HTTP methods, nested URLs vs filtering, and the anatomy of a request.

## 1. What is REST?

REST = Representational State Transfer.

It is a standard way for applications to communicate and transfer data:

- Frontend ↔ Backend
- One application ↔ another application

## 2. JSON Basics

REST normally sends data as JSON, a simple format made of key-value pairs.

```json
{
  "name": "Ash",
  "age": 25,
  "isActive": true,
  "address": { "city": "Pune" },
  "skills": ["Java", "React"],
  "nickname": null
}
```

Building blocks: objects `{ }` and arrays `[ ]`.

Value types allowed:

| Type | Example |
| --- | --- |
| String | `"Ash"` |
| Number | `25` |
| Boolean | `true` / `false` |
| Object (nested) | `{ "city": "Pune" }` |
| Array | `["Java", "React"]` |
| Null | `null` (no value) |

## 3. Endpoint = Method + Path

An endpoint is made of two things:

- Method (what to do)
- Path (what to do it on)

### Anatomy of a URL

```
https://mysite.com/api/v1/users
   │        │       │   │    │
 protocol domain   API  version resource
```

- Resource: the entity you work with (user, product, coupon, ...)
- Versioning (`v1`, `v2`) lets you change the API later without breaking old clients

In explanations we usually write only the resource part (`/users`) and assume the rest.

## 4. HTTP Methods (CRUD Operations)

| Operation | Method | Endpoint | What it does |
| --- | --- | --- | --- |
| Get all | GET | `/users` | Returns a list of users |
| Get one | GET | `/users/1` | Returns the user with ID 1 |
| Create | POST | `/users` | Adds a new user (data goes in the body) |
| Replace | PUT | `/users/1` | Replaces the whole user |
| Partial update | PATCH | `/users/1` | Updates only some fields |
| Delete | DELETE | `/users/1` | Deletes the user with ID 1 |

### PUT vs PATCH

Current user:

```json
{ "id": 1, "name": "Ash", "username": "ash", "age": 25 }
```

PUT with only the username:

```json
{ "username": "ak" }
```

The whole entity is replaced, so name and age become default or null. This is risky.

PATCH with only the username:

```json
{ "username": "ak" }
```

Only username changes. Everything else stays the same.

Rule: to update just a few fields, use PATCH. Use PUT only when sending the complete object.

## 5. Nested Data (Related Resources)

Example: a blog site with three related entities: users → blogs → comments.

A comment can't exist without a blog, so there is a clear relationship. We express it in the URL:

| Goal | Endpoint |
| --- | --- |
| All comments on a blog | `GET /blogs/{id}/comments` |
| All comments by a user | `GET /users/{id}/comments` |
| Update or delete one comment | `PUT` / `PATCH` / `DELETE /comments/{id}` |

### Nesting vs sending data in the body

You could do `GET /comments` and pass the `postId` in the request body. This works but is not recommended when there's a direct relationship. Nested URLs are easier to read and understand.

### Nesting vs filtering

| Use nesting when | Use filtering (query params) when |
| --- | --- |
| The relationship between two entities is clear and simple | The relationship is complex |
| Example: comments of a blog | Pagination, sorting, searching, multi-condition filters |
| `/blogs/5/comments` | `/products?color=red&price_max=500` |

Long nested paths get hard to handle, so don't nest deeply for filtering.

## 6. Three Ways to Pass Data to an Endpoint

### 1. Path

Use for the unique identifier: an ID or a slug.

```
/users/1
/blogs/what-is-java
```

- A slug is a short, readable, unique name for a post (e.g. `what-is-java`).
- Use plural resource names (`/blogs`, not `/blog`) because the endpoint covers many items.

### 2. Query parameters

Use for filtering, sorting, searching, and pagination.

```
/blogs?sort=asc          → oldest first
/blogs?sort=desc         → latest first
/blogs?q=java            → search for "java"
```

### 3. Body

Use for the data you send (create or update) and for sensitive information.

```json
POST /login
{
  "username": "ash",
  "password": "secret123"
}
```

Security rule: path and query parameters are visible (in URLs, logs, browser history). Never put sensitive data there. Use the body.

### Quick rule

| Where | Use for |
| --- | --- |
| Path | Identifying one resource (ID or slug) |
| Query params | Filter, sort, search, paginate |
| Body | Data to create or update, and anything sensitive |

## 7. Anatomy of a Full Request

```http
POST /api/v3/users
Content-Type: application/json

{
  "name": "Ash",
  "username": "ash",
  "age": 25
}
```

| Part | In the example | Meaning |
| --- | --- | --- |
| Method | POST | What action to perform |
| Path | `/api/v3/users` | Which resource (with API version) |
| Metadata (headers) | `Content-Type: application/json` | Extra information, such as the data format |
| Body | `{ ... }` | The actual data being sent |

The `Content-Type` header tells the server the data format. JSON is the most common. XML and newer formats are also possible.

## 8. Quick Summary

- REST uses JSON and HTTP methods to work with resources.
- Endpoint = method + path.
- Method meanings: GET read, POST create, PUT replace, PATCH partial update, DELETE remove.
- Use nested URLs for clear parent-child relationships and query params for filtering and sorting.
- Pass data via path (IDs), query (filters), or body (data and secrets).
- Use plural nouns for resources and version your APIs.

Next topics likely include HTTP status codes and API design best practices.
