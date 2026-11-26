# Types of Applications

Before choosing tools, first ask: what kind of application is this? Is it data-intensive or compute-intensive?

## Why Classify the Application First?

### The common mistake

When designing a system, most people jump straight to tools and diagrams:

"Here's the client, here's the database, let's add a cache..."

They skip the most important question: what is this application, and what are its limitations?

### The smart approach

Ask first: Is it a data-intensive or a compute-intensive application?

This one distinction:

- Saves cost
- Helps you fix the right problem

### Example: fixing latency

Latency = how long the system takes to respond.

Suppose two apps have the same users and the same network, and both suffer from high latency. Possible fixes:

- Add more databases
- Add or improve caching layers
- Upgrade the CPU or GPU

Which fix you pick depends on the type of application. A CPU upgrade will not help a database-bound app, and a bigger cache will not help a calculation-bound app.
