# Non-Functional Requirements

## Non-Functional Requirements

### What are they?

They define how the system performs: speed, scale, uptime, security, and so on. They are measurable targets, not features.

### Example: Amazon

| Requirement | Example target |
| --- | --- |
| Scale | Handle 1 million daily active users |
| Response time | Less than 200 ms per request (we must say how fast, not just "fast") |
| Availability | System is up 99.9% of the time (defined by SLAs and SLOs) |
| Security | Data is encrypted |
| Traffic spikes | Handle up to 10x normal traffic on sale days (Black Friday, Diwali, Holi) |
| Fault tolerance | The system keeps working despite failures, and we can detect and fix faults fast |

No system is perfect. Faults and downtime will happen, so we plan for them.

## The Generic Non-Functional Requirements

These apply to almost any system.

### 1. Scalability

Can the system handle growing traffic? When the current server hits its limit, do we scale horizontally (add servers) or vertically (upgrade the server)?

### 2. Availability

How much of the time is the system up?

- Measured by SLAs (Service Level Agreements) and SLOs (Service Level Objectives).
- Example: If you host on a cloud provider that promises a maximum of 5 minutes of downtime per day, that promise is written into a contract. If they break it, the customer company can take action, so availability is a serious commitment.

### 3. Reliability

The system should be dependable, with no data loss.

### 4. Performance

How fast does the system respond?

- Latency targets
- Percentile measures: P90, P95, P99

(Covered in detail in later chapters.)

### 5. Security

- Authentication (who are you?)
- Authorization (what are you allowed to do?)
- Encryption (protecting data)
- Modular code, so each part can use its own APIs or modules efficiently

### 6. Observability

After code goes to production, we don't know exactly how users will behave. So we need:

- Monitoring tools
- Logging
- Tools to track user behavior, so we can find bugs and improve the system

## Functional vs Non-Functional: Side by Side

| | Functional | Non-Functional |
| --- | --- | --- |
| Defines | What the system does | How well it does it |
| Focus | Features and user actions | Quality and performance |
| Examples | Login, search, add to cart, pay, track order | 1M users, under 200 ms, 99.9% uptime, encryption |
| Measured by | Does the feature exist and work? | Numbers and targets |

## Quick Checklist

Functional: list every feature the user can use.

Non-functional:

- [ ] Scalability
- [ ] Availability (SLAs / SLOs)
- [ ] Reliability (no data loss)
- [ ] Performance (latency, P90 / P95 / P99)
- [ ] Security (authentication, authorization, encryption)
- [ ] Observability (monitoring and logging)

## Practice Exercise

Pick an app you use daily (Instagram, YouTube, Netflix, WhatsApp, Flipkart...) and write down 3 to 4 functional and 3 to 4 non-functional requirements for it.

Note: the source transcript ends with the start of a new topic ("How does a browser know which web page to hit?"), which isn't included here. These notes cover everything up to that point.
