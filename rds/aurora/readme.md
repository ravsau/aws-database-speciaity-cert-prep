## Notes


### Security
- You can't convert an unencrypted DB cluster to an encrypted one. However, you can restore an unencrypted snapshot to an encrypted Aurora DB cluster. To do this, specify a CMK when you restore from the unencrypted snapshot.
  - You cannot create an encrypted copy of an unencrypted snapshot. However, this works for Amazon RDS.
  - https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Overview.Encryption.html#Overview.Encryption.Limitations


### How to delete Read Replica

Aurora MySQL clusters that are read replicas
For Aurora MySQL, you can't delete a DB instance in a DB cluster if both of the following conditions are true:

- The DB cluster is a read replica of another Aurora DB cluster.

- The DB instance is the only instance in the DB cluster.

To delete a DB instance in this case, first promote the DB cluster so that it's no longer a read replica. After the promotion completes, you can delete the final DB instance in the DB cluster. For more information, see Replicating Amazon Aurora MySQL DB clusters across AWS Regions.

https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/USER_DeleteInstance.html

---

### Note on Aurora reboot and Failover:
When you reboot the primary instance of an Amazon Aurora DB cluster, RDS also automatically restarts all of the Aurora Replicas in that DB cluster. When you reboot the primary instance of an Aurora DB cluster, no failover occurs. When you reboot an Aurora Replica, no failover occurs. To fail over an Aurora DB cluster, call the AWS CLI command failover-db-cluster, or the API operation FailoverDBCluster.


**Reboot with failover is an option with RDS (non Aurora)**
https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/USER_RebootInstance.html

- To simulate a failover, use fault injection queries
  - You can force a crash of an Amazon Aurora instance using the ALTER SYSTEM CRASH fault injection query.

  `ALTER SYSTEM CRASH [ INSTANCE | DISPATCHER | NODE ];`
---
