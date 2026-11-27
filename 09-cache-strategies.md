# Cache Strategies

## Cache Strategies

These strategies decide when data is written into the cache and when it is read from it.

```
Client ──> Backend ──> Cache ──> Database
```

### 1. Read-through cache (RTC)

Built for reads, not writes.

- A read always goes to the cache. The backend does not read the database directly.
- On a **hit**, the cache returns the value. Retrieval is fast.
- On a **miss**, the cache asks the database, receives the value, and returns it to the backend. That extra step makes the request slower.
- A write skips the cache and goes straight to the database.

```
Read:   Backend ──> Cache ──(miss only)──> Database
Write:  Backend ─────────────────────────> Database
```

Only data that users actually read ends up in the cache. An order that is written and never read again stays in the database. The cache stays filled with what people are asking for.

### 2. Write-through cache (WTC)

Built for writes.

A write goes to the cache first. The cache then writes that value into the database. The cache always holds the latest value.

```
Write:  Backend ──> Cache ──> Database
```

Use it where the latest value is what users must see, such as stock prices.

### 3. Write-around cache (WAC)

Covers both reads and writes.

- A write goes from the backend straight into the database. The cache is not updated on the write.
- A read always comes from the cache.
- On a **hit**, the cache returns the value.
- On a **miss**, the cache reads the database, stores the value, and then returns it.

```
Write:  Backend ─────────────────────────> Database
Read:   Backend ──> Cache ──(miss only)──> Database
```

Importance is decided when someone reads the data, not when it is created. Twitter (X) is the usual example. Lots of tweets are created, and a new tweet is not put in the cache at creation time. When a user opens that tweet, it is worth keeping, because other users may open it too.

### 4. Write-back cache (WBC)

A write is stored in the cache, and the write is treated as finished. The database is updated later, asynchronously.

```
Write:  Backend ──> Cache ──(async)──> Database
Read:   Backend ──> Cache ──(miss only)──> Database
```

This trades consistency for speed. The caller gets a fast response, and the database catches up afterward. The async write can fail, so this path has to be handled carefully.

Reads come from the cache. Because writes land in the cache first, the value is usually there (a hit). On a miss, the cache reads the database, updates itself, and returns the value.

The read path looks like write-around. The difference is the write: write-around writes the database immediately and skips the cache, while write-back writes the cache immediately and updates the database later.

Use write-back where writes are heavy and values change quickly. A food delivery app such as Swiggy or Zomato handles many orders, and each order's status changes often. Those status changes go into the cache so the update is fast and the customer sees the latest status. The database is updated in the background. That is how the system absorbs a large burst of status updates.

### Strategies at a glance

| Strategy | Write path | Read path | What you optimize for |
| --- | --- | --- | --- |
| Read-through | Straight to the database | Cache, then database on a miss | Fast reads of data people actually request |
| Write-through | Cache, then database | Latest value is already in the cache | Always seeing the newest value |
| Write-around | Straight to the database | Cache, then database on a miss | Caching data only after it is read |
| Write-back | Cache first, database later (async) | Cache, then database on a miss | Write speed over strict consistency |
