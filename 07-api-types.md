# Types of APIs

## Types of APIs

There are five main types.

### 1. REST

REST = Representational State Transfer

- The most common API style today
- Easy to use, well structured, and easy to maintain
- Usually sends data as JSON (JavaScript Object Notation), a simple, lightweight format

(The next chapter covers REST in more detail.)

### 2. SOAP

SOAP = Simple Object Access Protocol

- Uses XML to send data
- XML is bulky, because attributes must be repeated again and again. JSON fixed this problem, which is why JSON is preferred today.
- Still found in legacy systems that were built before JSON became popular.

If you work with a legacy system:

- Learn XML so you can work with it directly, or
- Use a middleware that converts XML into JSON for your app

### 3. GraphQL

GraphQL = Graph Query Language

- Exposes only one endpoint
- The frontend sends queries to that endpoint and asks for exactly the data it wants
- Similar in spirit to SQL, where you write different queries against one database
- Instead of hitting many endpoints (as in REST), the frontend uses one endpoint and many queries

### 4. gRPC

gRPC = Remote Procedure Calls (created by Google)

- Uses Protocol Buffers instead of JSON or XML
- Protocol Buffers are smaller and faster to transfer
- Commonly used for communication between microservices, where internal calls need to be fast and low-latency

```
Frontend ──(REST/GraphQL)──> Service A ──(gRPC)──> Service B ──(gRPC)──> Service C
```

### 5. WebSockets

- Used for real-time communication: chat, notifications, live quizzes, live updates
- Different from the others:

| Normal APIs (REST etc.) | WebSockets |
| --- | --- |
| Client sends a request, server responds | Client opens a channel that stays open |
| Only the client starts the conversation | Either side can send messages at any time |
| Client must keep asking ("any new messages?") | Server pushes updates by itself |

Once the channel is open, the backend can send chat messages or notifications immediately, with no repeated asking from the frontend.

## Comparison Table

| Type | Data Format | Key Idea | Best For |
| --- | --- | --- | --- |
| REST | JSON | Simple, structured endpoints | Most web and mobile apps |
| SOAP | XML | Older, bulky, strict | Legacy systems |
| GraphQL | JSON | One endpoint, flexible queries | Frontends that need custom data |
| gRPC | Protocol Buffers | Small and fast | Microservice-to-microservice calls |
| WebSockets | Varies | Two-way, open connection | Chat, notifications, live data |

## Key Takeaways

- APIs let applications share data and features safely, without exposing the database.
- They connect frontend to backend, and one application to another.
- Pick the API type based on the need:
  - General purpose → REST
  - Flexible queries from the frontend → GraphQL
  - Fast internal service calls → gRPC
  - Real-time two-way updates → WebSockets
  - Old system integration → SOAP / XML

Next topic: RESTful APIs in detail, including their parts, recommendations, and usage.
