# Cache

A cache is hardware or software that is used to store something, usually data, temporarily in a computing environment.
The cache server usually sits between the app server and database. If data is already in cache, there is no need to make a request to the database. It ensures low latency and high throughput.

## Why use cache?

1. Improve performance
   - Reading from memory is much faster than disk, about 50-200X
   - Can serve the same amount of traffic with fewer resources
   - Pre-calculate and cache data
   - Most apps have far more reads than writes, which is perfect for caching
1. Save money long-term

## Caching options

- Redis -- stores data as specific data types
- Memcached -- stores data as strings

Because Redis can change data in place without having to re-upload the entire data value, which reduces network overhead, it is usually preferred.

## Cache eviction

Cache eviction is the process of removing cached data to prevent 'stale' data. This means that if a user updates a piece of data and that data happens to be in cache, it is best to remove the cache data and retreive the new data from the database during the next read.

- Prevents stale data
- Caching only most valuable data to save resources

## Distributed cache

- Works like traditional cache
- Has built-in functionality to replicate data, shard data, across servers, and locate proper server for each key

## Why use distributed cache?

If data stores gets too large, we don't want the cache server to crash, so the way to circumvent this senario is to create shard the cached data into other cache servers that can be created on the fly.

You will likely have an active cache and a passive one. They are both exactly the same in terms of data, and they are constently in communication with each other to maintain consisentency. The best case would be to never have to use the passive, or back up, cache.

## TTL

Time to live for cache.

- Set a time period before a cache entry is deleted
- Used to prevent stale data
- Depends largely on use case: how important is consistency to your system?

## LRU/LFU

- Least recently used
  - Once cache is full, remove last accessed key and add new key
- Least frequently used
  - Track number of times key is accessed
  - Drop least used when cache is full

## Cache strategies

- Cache aside - most common

Data is lazy-loaded in cache then on next call if data is present then it will be a cache hit and the cache will return the data. If not, it will be a cache miss and the data will be retreived from the database. If data is updated in the database, thsi could cause an inconsistency in our cache and database, so to prevent this we set a TTL to the cache.

- Read through

The read through strategy is similar to the cache aside strategy. The main difference is that the cache in a read through strategy always automatically stays consistent with the database. A cache library or framework will maintain the consistency with the database. The data in this strategy is also lazy-loaded in the cache only when the user requests it. Also, the data model of the cache has to be consistent with the database since it is updated automatically by the library.

- Write through

Every write in this strategy goes through the cache before updating the database. This maintains high data consistency between the cache and database, but it adds some latency during the write operations since the data has to be additionally written to the cache. This is a good strategy for use cases where we need strict data consistency between the cache and the database. It can be used with other caching strategies to achieve optimized performance.

- Write back

This caching strategy helps reduce hosting costs significantly. The data is written to the cache instead of the database, and the cache, after some delay, as per the business logic, writes data to the database. This can help reduce costs but it is a riskier strategy. If the cache goes down before the database is updated, the data might get lost. Combining this strategy with other strategies would get the best of both worlds.
