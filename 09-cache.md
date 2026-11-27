# Cache

## Cache

### The problem

Every important piece of information is stored in a database and read back from it. A user opens telescope.com, the request reaches the backend, and the backend reads the database to build the page.

The homepage shows the most popular courses. Each course shows:

- A thumbnail (a static file)
- The name
- The price and the discounted price
- A few important sections

Those pieces do not all live in one table.

| What the page shows | Where it comes from |
| --- | --- |
| Name | `courses` |
| Price and discounted price | `prices` (they change by area and currency) |
| Important sections | `course_info` |
| Thumbnail | Static file storage |

Showing three courses means touching three tables and the static file store. Every user who opens the homepage repeats those reads.

If the homepage grows to six courses, one view makes 6 courses × 4 sources = 24 requests. At 10,000 daily active users, that is 10,000 × 6 = 60,000 course reads, each fanning out to those sources. The homepage gets slower, and the extra latency hurts the business. The same information should not be fetched from the database for every user.

### What a cache is

A cache is a memory store kept apart from the database. It can sit in the backend or in the frontend, and its job is to load repeated data faster.

The six homepage courses do not change on every request, so read them once and keep them in the backend, the frontend, or both. The next visit reads the cache instead of walking the tables again.

```
User ──> Backend ──> Cache ──(only on a miss)──> Database
```

### Where a cache can live

| Kind | Where it sits |
| --- | --- |
| Client-side cache | On the phone or in the browser |
| Server-side cache | In the backend |
| Database cache | Inside the database, holding the most requested rows so the tables themselves are not read every time |

### Cache hit, cache miss, and TTL

| Term | Meaning |
| --- | --- |
| Cache hit | The data is in the cache. The database is not touched. The response is faster. |
| Cache miss | The data is not in the cache. It has to be read from the database. The response is slower. |
| TTL (time to live) | How long a value stays in the cache. When the time is up, the entry expires and is removed so something else can take its place. |

Data is stored as a key-value pair. You look it up by the key. Each pair carries a TTL so the cache can tell whether that entry has expired.

### Why the cache stays small

The cache is faster because it holds only frequently used data, so it is much smaller than the database. The database holds everything the site needs.

Two reasons not to copy the whole database into the cache:

1. The useful set changes. Today the homepage campaign is Mastering Java. Tomorrow it is AI. The cache has to drop Java and hold AI, because users are asking for AI.
2. A search is fast in a small space and slow across the whole database. A cache as large as the database would make lookups slow, which removes the reason for having a cache: lower latency and better performance.

So the cache stays much smaller than the database, and its contents are refreshed so they stay relevant to users.
