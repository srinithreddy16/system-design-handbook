# RESTful Response

After a client sends a request, the server replies with a status code and a response body. This chapter covers both.

## 1. HTTP Status Codes

Status codes tell the client what happened with its request. They are grouped by their first digit.

| Range | Meaning |
| --- | --- |
| 2xx | Success |
| 3xx | Redirect |
| 4xx | Client error (the request has a problem) |
| 5xx | Server error (the backend has a problem) |

### The most common codes

| Code | Name | When to use it |
| --- | --- | --- |
| 200 | OK | Everything worked as expected |
| 201 | Created | A new entity was created (e.g. after POST) |
| 204 | No Content | Success, but nothing to send back (e.g. after a DELETE) |
| 301 | Moved Permanently | Permanent redirect |
| 302 | Found | Temporary redirect |
| 400 | Bad Request | The request body is wrong: validation failed, required fields missing, etc. |
| 401 | Unauthorized | The user isn't authenticated (not logged in or invalid credentials) |
| 403 | Forbidden | The user is logged in but not allowed to access this resource |
| 404 | Not Found | Wrong URL, or the resource doesn't exist |
| 500 | Internal Server Error | Something went wrong on the backend |

### Examples to remember

- **403:** You're logged into an LMS but haven't enrolled in a course, and you try to open its lesson video. You exist, but you're not allowed in.
- **404:** You request `/users/999` but no user has ID 999.
- **500:** A bug, a missing piece of logic, or a database connection problem in the backend.

### About 500 errors

Users shouldn't see why the server failed (database details, code errors, etc.). The user just gets a generic 500, and the team investigates using logs.

## 2. Response Body

A response body can contain:

- An array
- An object
- Nested objects

### Best practice: always return an object

Even if you're returning a list, wrap it in an object.

Not recommended (bare array):

```json
[
  { "id": 1, "name": "Ash" },
  { "id": 2, "name": "Ravi" }
]
```

Recommended (wrapped in an object):

```json
{
  "users": [
    { "id": 1, "name": "Ash" },
    { "id": 2, "name": "Ravi" }
  ]
}
```

Why?

It makes the API future-proof. If you later need to add more information, you just add a key. The structure doesn't change, so clients don't break.

```json
{
  "users": [ ... ],
  "userCount": 29
}
```

With a bare array, adding extra information would mean redesigning the whole response format.

## 3. Request to Response Map

### GET /users (get many)

| Case | Status | Body |
| --- | --- | --- |
| Success | 200 | `{ "users": [ ... ] }` |

### GET /users/1 (get one)

Don't return the user directly. Wrap it, for the same flexibility reason.

| Case | Status | Body |
| --- | --- | --- |
| Success | 200 | `{ "user": { "id": 1, "name": "Ash" } }` |
| ID doesn't exist | 404 | Error message |

### POST /users (create)

| Case | Status | Body |
| --- | --- | --- |
| Created | 201 | The new object or its ID |
| Invalid or missing data | 400 | Error message |
| Backend problem | 500 | Generic error |

### DELETE /users/1

| Case | Status | Body |
| --- | --- | --- |
| Deleted (with a message) | 200 | Optional message |
| Deleted (nothing to return) | 204 | None |
| ID doesn't exist | 404 | Error message |
| Not allowed to delete | 401 / 403 | Error message |
| Backend problem (e.g. unhandled dependencies) | 500 | Generic error |

## 4. Quick Cheat Sheet

```
2xx  → Success
     200 OK              → worked, here's the data
     201 Created         → new thing made
     204 No Content      → worked, nothing to return

3xx  → Redirect
     301 Permanent       → moved for good
     302 Temporary       → moved for now

4xx  → Your mistake (client)
     400 Bad Request     → invalid or missing data
     401 Unauthorized    → not logged in / not authenticated
     403 Forbidden       → logged in, but no permission
     404 Not Found       → doesn't exist

5xx  → Our mistake (server)
     500 Internal Server Error → backend problem
```

## 5. Key Takeaways

- Always send the right status code, because it tells the client what happened.
- Always wrap response data in an object, even for arrays and single items.
- Hide internal error details from users. Log them for the team instead.
- Use 201 for creation, 204 when there's nothing to return, and 404 for missing resources.

This completes the REST request and response sections.
