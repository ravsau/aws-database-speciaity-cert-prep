# RDS Highlights


- You can create an Aurora Read Replica of a non Aurora RDS DB. And promote that replica to be the Aurora Master DB.
  - https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Migrating.RDSMySQL.Replica.html
- You can migrate a DB snapshot of an Amazon RDS MySQL DB instance to create an Aurora MySQL DB cluster. The new Aurora MySQL DB cluster is populated with the data from the original Amazon RDS MySQL DB instance.
-  You can migrate data directly from an Amazon RDS PostgreSQL DB snapshot to an Aurora PostgreSQL DB cluster.
  - https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraPostgreSQL.Migrating.html
- You can also create a Aurora PostgreSQL Cluster using RDS Postgres snapshot.

- Read Replica uses Async Replication
- Multi-AZ setup uses Synchronous replication


## RDS Storage Autoscaling
- RDS Storage Auto Scaling automatically scales storage capacity in response to growing database workloads, with zero downtime.

    Previously, you had to manually provision storage capacity based on anticipated application demands. Under-provisioning could result in application downtime, and over-provisioning could result in underutilized resources and higher costs. With RDS Storage Auto Scaling, you simply set your desired maximum storage limit, and Auto Scaling takes care of the rest.




## Migration from On-prem to AWS Aurora:
- mysql dump is slow. You can use a Percona backup software --> Save files to S3 --> Import files to create an Aurora Cluster. This method is lot faster than mysqldump.
- https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Migrating.ExtMySQL.html




## Other things to note:
- When you restore a DB instance, the default security group is associated with the restored instance by default.
  - https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_RestoreFromSnapshot.html
- To use Performance Insights, enable it on your DB instance. If needed, you can disable it later. Enabling and disabling Performance Insights doesn't cause downtime, a reboot, or a failover.
  - https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PerfInsights.Enabling.html



---
RDS ( non-aurora) Read reaplica Load Balancing

- Non-Aurora RDS doesn't provide a read replica endpoint that balances the load across instances like Aurora does with the Read Replica Endpoint. The way to configure load balancing is by using Route53.
  - You can use Amazon Route 53 weighted record sets to distribute requests across your read replicas. Within a Route 53 hosted zone, create individual record sets for each DNS endpoint associated with your read replicas and give them the same weight. Then, direct requests to the endpoint of the record set.

    - https://aws.amazon.com/premiumsupport/knowledge-center/requests-rds-read-replicas/
