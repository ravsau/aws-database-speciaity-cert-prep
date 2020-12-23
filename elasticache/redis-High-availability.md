https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/AutoFailover.html

## Minimizing Downtime in ElastiCache for Redis with Multi-AZ



- In certain cases, ElastiCache for Redis detects and replaces a primary node. These cases include certain types of planned maintenance and the unlikely event of a primary node or Availability Zone failure.

- This replacement results in some downtime for the cluster. If you have Multi-AZ enabled on the cluster, the downtime is minimized. In this case, the role of primary node fails over to one of the read replicas. There's no need to create and provision a new primary node. This failover and replica promotion ensure that you can resume writing to the new primary as soon as promotion is complete.

- ElastiCache also propagates the Domain Name Service (DNS) name of the promoted replica. It does so because then if your application is writing to the primary endpoint, no endpoint change is required in your application. If you are reading from individual endpoints, make sure that you change the read endpoint of the replica promoted to primary to the new replica's endpoint.

- In case of planned node replacements initiated due to maintenance updates or self-service updates, be aware of the following:

    - For ElastiCache for Redis Cluster, the planned node replacements complete while the cluster serves incoming write requests.

    - For Redis Cluster mode disabled clusters with Multi-AZ enabled that run on the 5.0.5 or later engine, the planned node replacements complete while the cluster serves incoming write requests.

    - For Redis Cluster mode disabled clusters with Multi-AZ enabled that run on the 5.0.4 or earlier engine, you might notice a brief write interruption associated with DNS updates. This interruption might take up to a few seconds. This process is much faster than recreating and provisioning a new primary, which is the process if you don't enable Multi-AZ.

You can enable Multi-AZ using the ElastiCache Management Console, the AWS CLI, or the ElastiCache API.

Enabling ElastiCache Multi-AZ on your Redis cluster (in the API and CLI, replication group) improves your fault tolerance. This is true particularly in cases where your cluster's read/write primary cluster becomes unreachable or fails for any reason. Multi-AZ is only supported on Redis clusters that have more than one node in each shard.
