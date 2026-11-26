# Data Intensive Application

## Data-Intensive Applications

### What is it?

The core focus is data: storing it, gathering it, moving it, and constantly updating it. The calculations are simple. The job is mostly to move data from the database to the client quickly.

Most applications you will work on are data-intensive.

### Where the bottlenecks are

| Bottleneck | Example |
| --- | --- |
| Database | Slow responses |
| Network | Heavy or unoptimized network calls |
| Server | Low configuration |

We do not blame or upgrade the CPU. We fix the database, the network calls, and the server.

### Common examples

- Instagram feed
- WhatsApp messages (millions of messages per day)
- Bank transactions
- Analytics dashboards
- Log processing systems

### Main worries

- How fast can we read data?
- How safely can we store data?
- How many users can use the same data at the same time?
- What if something fails? (a server, a network call, or a database machine goes down)

### Tools used to solve these

- Databases
- Caching
- Replication
- Sharding
- Data consistency

(Each of these is covered in later chapters.)

### Case study: Instagram feed

What it does (no complex math):

- Fetch posts
- Sort by time or relevance
- Show images and videos
- Let users like, comment, and share

The challenge: Millions of users are reading and writing at the same time, with millions of pieces of content.

How Instagram scales:

- Multiple databases to store data
- Aggressive caching to fetch data fast
- CDN for images and videos. The database stores only the location of the file, and the CDN serves the actual file.

Key insight: Instagram barely touches the CPU or GPU to scale. The problem is data movement between components, not computation.
