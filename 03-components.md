# Components of System Design

These are the building blocks that show up in almost every system, from Instagram and YouTube to Netflix and Amazon.

## 1. Data Is at the Core

Every app we use shows us data in one of four forms:

- Images
- Videos
- Audio
- Text

System design is mostly about storing this data and making it available to users the way they expect it.

## 2. The 7 Components

### Component 1: Database

What it does: Stores data and lets us retrieve it later.

- Drawn as a cylinder in diagrams.
- Two broad categories: SQL and NoSQL. Each has many specific databases to choose from.
- Whatever you pick, the core job is the same: save data and fetch it.

(SQL vs NoSQL is covered in detail in later chapters.)

### Component 2: Application Code (Server)

Why we need it: Imagine every user had to write database queries themselves. They'd need to know how all the tables (SQL) or documents (NoSQL) are structured. For a big system like LinkedIn, data is spread across many tables, so that is impossible for ordinary users.

What it does: Sits in front of the database and hides its complexity. It exposes APIs (endpoints) so the outside world can ask for data without touching the database directly.

Typical operations through endpoints:

| Operation | Meaning |
| --- | --- |
| Insert | Create new data |
| Retrieve | Read data |
| Update | Change existing data |
| Delete | Remove data |

Example: A GET endpoint like `https://telescope.com/students` returns all students.

How the app code and database connect: IP addresses, HTTP, TCP, and so on. Data is usually sent and received as JSON.

Logic and data are now separated: the application code holds the logic, the database holds the data.

### Component 3: Client Application

Why we need it: Even with APIs, calling endpoints and reading JSON is tedious for normal users. A client app makes this easy.

Examples of clients: mobile app, web app, desktop app, even an ATM machine.

How it fits together:

```
Client (mobile / web)  ──>  Application Code (on a server)  ──>  Database
```

- The client talks to the server over HTTP, TCP, or IP.
- The application code must be hosted on a server so clients can reach it.
- Because it exposes APIs, other applications and servers can also use it, not just our own client.
- Most communication starts from the client and flows toward the database.

This is the basic architecture of simple projects such as a to-do app or a chat app.

### Component 4: Cache

The problem: Every request goes to the database, and database calls are heavy. A query that joins data from, say, 12 tables takes time.

The fix: A cache is a fast storage layer that holds frequently used data. If the data is in the cache, we skip the database call.

```
Client ──> Application Code ──> Cache ──(if data not found)──> Database
```

Questions like when to put data into the cache and when to remove it are decided by caching strategies, covered in later chapters.

### Component 5: Load Balancer

The problem: A big app runs on multiple servers (Server 1, Server 2, ...). Who decides which server a request goes to?

The fix: A load balancer sits in the middle and handles every request. It has two jobs:

- Health check. Is each server working?
- Distribute traffic. Split requests evenly across servers.

```
Client ──> Load Balancer ──┬──> Server 1
                           └──> Server 2
```

### Component 6: Message Queue (Message Broker)

The scenario: When you place an order, many tasks happen:

- Update inventory
- Process the order
- Arrange delivery with the vendor
- Send an email or SMS confirmation

We can't make every service wait for every other service to respond.

Two types of calls:

| Type | How it works |
| --- | --- |
| Synchronous | Order service sends a request and waits for a confirmation before moving on |
| Asynchronous | Order service sends the request and moves on without waiting |

Where the message queue comes in (for async):

```
Order Service ──> [ Message Queue ] ──> SMS Service
```

The order service drops its request into the queue and forgets about it. The queue takes over:

- Stores every incoming request
- Delivers them to the target service one by one
- Retries if a request fails
- Reports back on request status (for example a batch update at the end of the day)

Message queues are especially important when you have many microservices talking to each other.

### Component 7: Monitoring and Logs

Why: A real system has many parts: clients, load balancer, servers, multiple databases (which also talk to each other), third-party services, and message queues. We need to know if each is working.

What we need to be able to do:

- Check that the load balancer and other components are healthy
- Spot errors in the application code
- See the full stack trace of an error
- Reproduce the error locally so we can fix it
- Check that adding a new feature doesn't break existing ones

Tools: Monitoring tools and logs. Testing teams also play a big role here.

## 3. Full Architecture (All Components Together)

```
        Client (mobile / web)
                │  API
                ▼
         Load Balancer
          ┌─────┴─────┐
          ▼           ▼
       Server 1    Server 2     (application code)
          └─────┬─────┘
        ┌───────┼────────────┐
        ▼       ▼            ▼
      Cache  Database(s)  Message Queue ──> Third-party / other services

   Monitoring and Logs watch over everything
```

## 4. Quick Reference Table

| # | Component | Problem it solves |
| --- | --- | --- |
| 1 | Database | Where to store and retrieve data |
| 2 | Application code | Users can't query databases directly, so it hides complexity behind APIs |
| 3 | Client app | Normal users can't call APIs by hand |
| 4 | Cache | Database calls are slow for frequently used data |
| 5 | Load balancer | Which server gets which request, and are the servers healthy? |
| 6 | Message queue | Services shouldn't wait on each other (async communication) |
| 7 | Monitoring and logs | Knowing when something breaks, and why |

## 5. Key Terms

- **API / Endpoint:** a URL through which clients request or change data
- **JSON:** the common format for sending data to and from APIs
- **HTTP / TCP / IP:** ways components communicate over a network
- **Synchronous call:** wait for a response before continuing
- **Asynchronous call:** send the request and continue without waiting
- **Microservice:** a small, independent service handling one job (order, SMS, ...)
- **Stack trace:** the detailed error trail that shows where code failed

Note: the source transcript ends mid-sentence, so these notes cover everything up to that point.
