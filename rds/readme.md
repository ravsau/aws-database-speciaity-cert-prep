# RDS Highlights 


- You can create an Aurora Read Replica of a non Aurora RDS DB. And promote that replica to be the Aurora Master DB. 
  - https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Migrating.RDSMySQL.Replica.html
- You can migrate a DB snapshot of an Amazon RDS MySQL DB instance to create an Aurora MySQL DB cluster. The new Aurora MySQL DB cluster is populated with the data from the original Amazon RDS MySQL DB instance. 
-  You can migrate data directly from an Amazon RDS PostgreSQL DB snapshot to an Aurora PostgreSQL DB cluster.
  - https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraPostgreSQL.Migrating.html
- You can also create a Aurora PostgreSQL Cluster using RDS Postgres snapshot. 

- Read Replica uses Async Replication 
- Multi-AZ setup uses Synchronous replication




## Migration from On-prem to AWS Aurora: 
- mysql dump is slow. You can use a Percona backup software --> Save files to S3 --> Import files to create an Aurora Cluster. This method is lot faster than mysqldump. 
- https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/AuroraMySQL.Migrating.ExtMySQL.html

