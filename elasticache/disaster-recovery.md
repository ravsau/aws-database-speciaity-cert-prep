### Replication Across AWS Regions Using Global Datastores

TLDR: You can use Redis Global Datastore for cross region read replica and Disaster Recovery


- By using the Global Datastore for Redis feature, you can work with fully managed, fast, reliable, and secure replication across AWS Regions. Using this feature, you can create cross-Region read replica clusters for ElastiCache for Redis to enable low-latency reads and disaster recovery across AWS Regions.


## Overview
Each global datastore is a collection of one or more clusters that replicate to one another.

A global datastore consists of the following:

- Primary (active) cluster – A primary cluster accepts writes that are replicated to all clusters within the global datastore. A primary cluster also accepts read requests.

- Secondary (passive) cluster – A secondary cluster only accepts read requests and replicates data updates from a primary cluster. A secondary cluster needs to be in a different AWS Region than the primary cluster.

https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/Redis-Global-Datastore.html
