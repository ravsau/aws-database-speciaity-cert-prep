# Document DB Notes
Whitepaper: https://d1.awsstatic.com/whitepapers/getting-started-with-amazon-documentdb.pdf?did=wp_card&trk=wp_card

# Document DB Architecture


#### Cluster:
 A cluster consists of one or more instances that provide the compute,
and a cluster volume that manages the data for the instances. A cluster can
have up to 16 instances (a primary and up to 15 read replicas). Cluster
instances need not be all of the same instance size.



#### Primary instance:

An instance that supports read/write workloads and performs
all the data modifications to the cluster volume. Each Amazon DocumentDB
cluster has one primary instance.
####  Cluster volume:

 The cluster volume provides SSD-backed storage for your
database. The primary instance and any Amazon DocumentDB replicas share
the same cluster volume.
####  Replicas:

An Amazon DocumentDB replica supports only read operations, and
each DB cluster can have up to 15 Amazon DocumentDB replicas. In case the
primary instance fails, one of the Amazon DocumentDB replicas is promoted as
the primary.


--------


### Highly Available Distributed Storage
Amazon DocumentDB replicates your data six ways across three Availability Zones.
The cluster volume spans three Availability Zones in a single AWS Region, and each
Availability Zone contains two copies of the cluster volume data. This functionality
means that Amazon DocumentDB can transparently handle the loss of up to two data
copies or an Availability Zone failure without losing write availability, or the loss of up to
three data copies without losing read availability.

###  Auditing Events
Amazon DocumentDB supports auditing of the operations performed on your cluster.
Once auditing is enabled, Amazon DocumentDB tracks authentication, Data Definition
Language (DDL), and user management events. For example, with the auditing feature,
you can track failed login attempts, or DDL operations like the creation of collections or
indexes. These audit records are exported as JSON documents to Amazon CloudWatch
Logs for you to analyze and monitor.

### User Management
You can connect to Amazon DocumentDB using standard MongoDB tools and drivers.
Amazon DocumentDB supports authentication using the Salted Challenge Response
Authentication Mechanism (SCRAM), which is the default authentication mechanism
with MongoDB.
When you create an Amazon DocumentDB cluster, you specify a master user name
and password. The master user has administrative permissions for the cluster. You can
connect as the master user to Amazon DocumentDB and create additional users as
required using db.createUser.


### Quorum-based Reads and Writes
I/O operations use distributed systems techniques such as quorums to improve
performance consistency and tolerance to outliers. Data write operations are
acknowledged as soon as they are committed by four out of six storage nodes, and
individual storage nodes acknowledge the write operations as soon as the log records
are persisted to disk. A slow or failed storage node does not impact database
performance or availability due to the use of the quorum model.

### Failover Tiers
Each Amazon DocumentDB replica instance is associated with a failover tier (0–15).
When a failover occurs due to maintenance or an unlikely hardware failure, the primary
instance fails over to a replica with the lowest numbered priority tier. If multiple replicas
have the same priority tier, the primary fails over to that tier's replica that is the closest
in size to the primary.
By setting the failover tier for a group of select replicas to 0 (the highest priority), you
can ensure that a failover promotes one of the replicas in that group. Further, you can
effectively prevent specific replicas from being promoted to primary if there is a failover
by assigning a low-priority tier (high number) to these replicas. This is useful in cases
where specific replicas are receiving heavy use by an application and failing over to one
of them would negatively affect a critical application.
