## Caching Strategies

In the following topic, you can find strategies for populating and maintaining your cache.

What strategies to implement for populating and maintaining your cache depend upon what data you cache and the access patterns to that data. For example, you likely don't want to use the same strategy for both a top-10 leaderboard on a gaming site and trending news stories. In the rest of this section, we discuss common cache maintenance strategies and their advantages and disadvantages.

## 1) Lazy Loading
As the name implies, lazy loading is a caching strategy that loads data into the cache only when necessary. It works as described following.

Amazon ElastiCache is an in-memory key-value store that sits between your application and the data store (database) that it accesses. Whenever your application requests data, it first makes the request to the ElastiCache cache. If the data exists in the cache and is current, ElastiCache returns the data to your application. If the data doesn't exist in the cache or has expired, your application requests the data from your data store. Your data store then returns the data to your application. Your application next writes the data received from the store to the cache. This way, it can be more quickly retrieved the next time it's requested.

### The advantages of lazy loading are as follows:

- Only requested data is cached.

- Because most data is never requested, lazy loading avoids filling up the cache with data that isn't requested.

- Node failures aren't fatal for your application.

- When a node fails and is replaced by a new, empty node, your application continues to function, though with increased latency. As requests are made to the new node, each cache miss results in a query of the database. At the same time, the data copy is added to the cache so that subsequent requests are retrieved from the cache.

### The disadvantages of lazy loading are as follows:

- There is a cache miss penalty. Each cache miss results in three trips:

  - Initial request for data from the cache

  - Query of the database for the data

  - Writing the data to the cache

These misses can cause a noticeable delay in data getting to the application.

- Stale data.

    - If data is written to the cache only when there is a cache miss, data in the cache can become stale. This result occurs because there are no updates to the cache when data is changed in the database. To address this issue, you can use the Write-Through and Adding TTL strategies.
----


## 2) Write-Through
- The write-through strategy adds data or updates data in the cache whenever data is written to the database.

### The advantages of write-through are as follows:

- Data in the cache is never stale.

- Because the data in the cache is updated every time it's written to the database, the data in the cache is always current.

- Write penalty vs. read penalty.

- Every write involves two trips:

      - A write to the cache

      - A write to the database

Which adds latency to the process. That said, end users are generally more tolerant of latency when updating data than when retrieving data. There is an inherent sense that updates are more work and thus take longer.

### The disadvantages of write-through are as follows:

- Missing data.

  - If you spin up a new node, whether due to a node failure or scaling out, there is missing data. This data continues to be missing until it's added or updated on the database. You can minimize this by implementing lazy loading with write-through.

- Cache churn.

  - Most data is never read, which is a waste of resources. By adding a time to live (TTL) value, you can minimize wasted space.
