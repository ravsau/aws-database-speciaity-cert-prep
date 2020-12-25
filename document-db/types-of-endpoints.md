Whitepaper: https://d1.awsstatic.com/whitepapers/getting-started-with-amazon-documentdb.pdf?did=wp_card&trk=wp_card


## Cluster Endpoint
The cluster endpoint connects to your cluster’s current primary instance. The cluster
endpoint can be used for read and write operations. The cluster endpoint provides
failover support. If your cluster’s current primary instance fails, the cluster endpoint
automatically redirects connection requests to a new primary instance. You do not have
to make changes to your application after a failover.
## Reader Endpoint
The reader endpoint load balances read-only connections across all available replicas
in your cluster including the primary instance. When you add a replica instance to your
Amazon DocumentDB cluster, it is made available for load balancing read connections
using the reader endpoint. This means that you do not have to make any application
changes while adding or removing read replicas in your cluster.
## Instance Endpoint
You can also connect to any instance in your cluster using the instance endpoint. The
recommended way to connect to your cluster is to use the cluster endpoint for
read/write operations and the reader endpoint for read operations. However, there may
be scenarios where you create a larger than normal read replica for running analytic
workloads. You can use the instance endpoint to connect and run those analytical
queries against the larger instance without affecting other instances in the cluster.
See the Amazon DocumentDB documentation for step-by-step instructions on creating
an Amazon DocumentDB cluster and connecting to it.
