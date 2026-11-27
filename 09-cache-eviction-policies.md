# Cache Eviction Policies

## Cache Eviction Policies

The strategies above decide how data gets into the cache. Eviction policies decide what leaves when the cache needs room.

The cache has a fixed size. Once it is full, something already stored has to go before a new value can come in.

### 1. LRU (Least Recently Used)

Remove the data that has not been used for the longest time.

Example: a new iPhone is what everyone searches for. Almost nobody still searches for an iPhone 11. The older phone is stale, so it is the one that leaves the cache.

### 2. MRU (Most Recently Used)

Remove the data that was used most recently.

That sounds backwards, and it fits a few cases:

- An e-commerce user has already applied a coupon. That coupon does not need to stay in the cache.
- A video streams in sections. The player loads ahead of the playhead (the buffered part of the bar). Once a section has been watched and the next section is loaded, the earlier section can leave the cache, because the viewer rarely scrubs backward.

### 3. LFU (Least Frequently Used)

Remove the data that has been used the fewest times.

Example: on a shopping app you often open secondary screens and the clothes section, but you searched for a plant only once. The plant is the least frequent item, so it is evicted first.

### 4. FIFO (First In, First Out)

Remove the entry that was inserted first.

Suppose the cache is capped at 180 MB and a new value would pass that limit. FIFO drops the oldest entry. It does not look at how often the entry was used or how recently.

### 5. LIFO (Last In, First Out)

Remove the entry that was inserted last, the way a stack pops its top item.

With the same 180 MB cap, the newest value is the one removed. The earliest entries stay the longest, and recent ones are dropped to free space.

The lecture does not give product examples for FIFO and LIFO.

### Policies at a glance

| Policy | What gets removed | Example |
| --- | --- | --- |
| LRU | Least recently used | Old phone model nobody searches anymore |
| MRU | Most recently used | A coupon already applied, or a video segment already watched |
| LFU | Least frequently used | A one-time search among many repeat searches |
| FIFO | Oldest entry | First value in, first value out, once the size limit is hit |
| LIFO | Newest entry | Last value in, first value out |
