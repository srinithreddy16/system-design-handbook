# Compute Intensive Application

## Compute-Intensive Applications

### What is it?

The exact opposite. The amount of data fetched from the database is small, but the calculations are heavy.

Our focus moves away from database, caching, replication, and sharding. It moves to the CPU and GPU.

These systems are called compute-bound (or CPU-bound / GPU-bound).

### Common examples

- Image processing
- Video rendering
- Machine learning model training
- Simulations
- Cryptography

### Main worries

- How fast can we compute?
- Can we do work in parallel? (For example, an image processes in the background while you keep using the app.)
- How can we reduce computational cost?
- Can we use a GPU instead of a CPU?

### Case study: Flight simulator

Pilots are trained on simulators before flying real aircraft, since real planes are expensive. The simulator must behave exactly like the real machine, which needs heavy calculation.

Worries for the simulator:

- Can anything run in parallel?
- Can we use a GPU instead of a CPU?
- How do we reduce the cost?
- Which good algorithms can we use to do the calculations efficiently?

## Side-by-Side Comparison

| | Data-Intensive | Compute-Intensive |
| --- | --- | --- |
| Core focus | Storing, moving, and serving data | Heavy calculation |
| Data from DB | Large | Small |
| Calculation | Simple | Heavy |
| Bottleneck | Database, network, server | CPU / GPU |
| Key worries | Read speed, safe storage, concurrent users, failures | Compute speed, parallelism, cost, GPU use |
| Tools / fixes | Caching, replication, sharding, consistency, CDN | Better algorithms, parallel processing, GPUs |
| Examples | Instagram feed, WhatsApp, banking, logs | Video rendering, ML training, simulation, cryptography |

## Important Points to Remember

### 1. Put effort in the right place

Components are not free. If you spend money on the wrong component (for example a GPU for a database-bound app), it won't solve the problem and will make the design worse.

### 2. One app can be both

A single application often has both kinds of features. The type depends on the feature.

Example: YouTube

- Serving videos is data-intensive
- Recommendations are compute-intensive

### 3. The quick trick

Where is the time being lost?

- Lost in data movement → data-intensive
- Lost in computation → compute-intensive

This one distinction saves money, time, and complexity.

Note: the source transcript ends mid-sentence, just as it begins to introduce functional vs non-functional requirements. These notes cover everything up to that point.
