# Application Programming Interface (API)

What an API is, why we use one instead of exposing the database, and the five main API styles.

## Chapter 14: What is an API?

API = Application Programming Interface. It is the set of endpoints an application exposes so that other programs can use its data or features.

### Real-world example

Uber, Ola, Rapido, and Swiggy all show maps inside their apps. They didn't build their own maps. They use Google Maps' APIs.

### Use Case 1: Another application uses your data

Say you have a movie app (like IMDb) with movies, ratings, and reviews stored in your database. Someone else wants to build an app using that data.

Option A: Build everything from scratch and collect all the ratings and reviews again. This is wasteful.

Option B: Call your app's APIs and get the data directly. This is faster and saves a lot of work.

They can also use your other endpoints, for example one that lets users write a review, instead of building the same feature again.

```
Developer's App  ──(API call)──>  Movie App  ──>  Movie App's Database
```

### Use Case 2: Your own frontend uses your backend

A single application is often split into:

- Frontend: web or mobile app (React, etc.)
- Backend: server with the logic and data (any language)

The frontend calls the backend's APIs. It doesn't care what language the backend is written in, as long as it can call APIs.

### Why not give direct database access?

Letting outsiders like other applications backend (or even your own frontend) touch the database is dangerous:

- They might delete or corrupt important data, which affects every other app using it.
- They'd need to handle complex database queries themselves.
- It's a security risk.

The API is a safe gate in front of the database. People can only do what the endpoints allow.

### Open vs restricted APIs

You decide who can use your APIs:

- Restricted: only your own frontend can call them
- Open: other applications can use them too
- Both can be true at the same time
