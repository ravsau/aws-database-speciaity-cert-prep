- MySQL Replica Lag
  - Amazon RDS for MySQL uses asynchronous replication and sometimes the replica isn't able to keep up with the primary DB instance. This can cause replication lag.

  - When using an Amazon RDS for MySQL read replica with binary log file position-based replication, you can monitor replication lag in Amazon CloudWatch by viewing the Amazon RDS ReplicaLag metric. The ReplicaLag metric reports the value of the Seconds_Behind_Master field of the SHOW SLAVE STATUS command.

  - The Seconds_Behind_Master shows the difference between the current timestamp on the replica DB instance and the original timestamp logged on the primary DB instance for the event that is being processed on the replica DB instance.
  - https://aws.amazon.com/premiumsupport/knowledge-center/rds-mysql-high-replica-lag/
