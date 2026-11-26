# The Alien Bank Analogy

A bank story is used to explain core system design concepts: scaling, databases, and load balancing.

## 1. The Setup

Alien Bank has one cash counter with one cashier.

Customer flow (4 steps):

1. Customer comes to the counter
2. Customer withdraws or deposits money
3. Cashier gives a receipt
4. Transaction is done

Simple on purpose. Now we hit 5 problems and fix them one by one. Each fix teaches a system design concept.

## 2. The 5 Issues and Their Fixes

### Issue 1: The process is slow

Cashier takes 10 min per customer, so only 6 customers per hour. Rush hour would break the system.

Where the time goes:

- Understanding what the customer wants (deposit or withdraw)
- Counting cash by hand
- Writing the receipt

Fix: Train the cashier (count cash faster, type faster). No new resources added.

Result: 10 min drops to 5 min per customer (50% improvement).

System design version: Improve the code. Better algorithms, cleaner logic, faster loops. This is where LLD (low-level design) and DSA come in.

### Issue 2: Customer count is growing

The cashier is already at peak performance, so we can't train them any further. Instead we upgrade their environment:

- Bigger desk
- Cash counting machine (no manual counting)
- Forms given in advance, so customers fill in what they want before reaching the counter

Result: 5 min drops to 3 min per customer.

System design version: Upgrade the machine (more CPU, RAM, better hardware). This is Vertical Scaling.

Vertical scaling has a hard limit. After a point, you can't upgrade one machine any more.

### Issue 3: Customers still wait too long

Cashier and counter are both maxed out. With 10 customers, the 10th waits 27 minutes. The root cause is a single counter.

Fix: Add more counters (Counter 1, Counter 2, ...).

System design version: Add more servers. This is Horizontal Scaling.

### Issue 4: Data is out of sync

Each counter keeps its own records, which causes two problems:

- Counter 2 doesn't know about a customer who is valid at Counter 1.
- A customer withdraws at Counter 1, then withdraws the same money again at Counter 2 (data discrepancy).

Fix: One centralized database that both counters read from and write to.

```
Counter 1 ──┐
            ├──> Central Database
Counter 2 ──┘
```

System design version: A shared/centralized database (or a distributed database architecture) so all servers see the same data.

### Issue 5: Underutilized counter

The bank gate is closer to Counter 1, so most customers go there while Counter 2 sits idle. That means longer waits and wasted capacity.

Fix: Add a middleman at the entrance.

- Customers talk to the middleman first.
- The middleman checks how busy each counter is and sends the customer to the less busy one.
- If Counter 1 breaks, the middleman sends everyone to Counter 2 until it's fixed.

System design version: A Load Balancer, which does two jobs:

- Health checks. Is each server working?
- Distribution. Spread requests evenly across healthy servers.

## 3. Final Architecture

```
Customers (requests / traffic)
        │
        ▼
 Middleman (Load Balancer)
        │
   ┌────┴────┐
   ▼         ▼
Counter 1  Counter 2   (Servers running application code)
   └────┬────┘
        ▼
 Centralized Database
```

## 4. Analogy Cheat Sheet

| Alien Bank | System Design |
| --- | --- |
| Customers | Requests |
| Customers waiting in line | Traffic / queue |
| Cash counter | Server |
| Cashier | Application code |
| Training the cashier | Optimizing code (LLD, DSA) |
| Bigger desk, cash machine | Vertical scaling |
| Adding more counters | Horizontal scaling |
| Shared ledger | Centralized database |
| Middleman at the entrance | Load balancer |
| Middleman skipping a broken counter | Health checks / fault tolerance |

## 5. Key Concepts Summary

| Problem | Solution | Concept |
| --- | --- | --- |
| Slow processing | Make the work itself faster | Code optimization (LLD, DSA) |
| Growing load on one machine | Upgrade the machine | Vertical scaling (limited) |
| One server can't keep up | Add more machines | Horizontal scaling |
| Servers have different data | Shared data store | Centralized database |
| Uneven traffic across servers | Distribute and monitor | Load balancer |

### Vertical vs Horizontal Scaling

| | Vertical | Horizontal |
| --- | --- | --- |
| What you do | Make one server stronger | Add more servers |
| Limit | Yes, hardware ceiling | Much higher |
| Complexity | Low | Higher (needs a load balancer, shared data) |

## 6. Takeaway

Real apps (WhatsApp, Snapchat, etc.) follow this same pattern:

1. Write efficient code
2. Scale up (vertical) until you hit the limit
3. Scale out (horizontal) with more servers
4. Keep data consistent with a shared database
5. Use a load balancer to spread traffic and avoid failed servers

Note: the source transcript ends mid-sentence while moving on to real-world apps, so these notes cover everything up to that point.
