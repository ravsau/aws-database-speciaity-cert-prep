Documentation: 


## Types of Aurora endpoints<a name="Aurora.Overview.Endpoints.Types"></a>

 An endpoint is represented as an Aurora\-specific URL that contains a host address and a port\. The following types of endpoints are available from an Aurora DB cluster\. 

**Cluster endpoint**  
 A *cluster endpoint* \(or *writer endpoint*\) for an Aurora DB cluster connects to the current primary DB instance for that DB cluster\. This endpoint is the only one that can perform write operations such as DDL statements\. Because of this, the cluster endpoint is the one that you connect to when you first set up a cluster or when your cluster only contains a single DB instance\.   
 Each Aurora DB cluster has one cluster endpoint and one primary DB instance\.   
 You use the cluster endpoint for all write operations on the DB cluster, including inserts, updates, deletes, and DDL changes\. You can also use the cluster endpoint for read operations, such as queries\.   
 The cluster endpoint provides failover support for read/write connections to the DB cluster\. If the current primary DB instance of a DB cluster fails, Aurora automatically fails over to a new primary DB instance\. During a failover, the DB cluster continues to serve connection requests to the cluster endpoint from the new primary DB instance, with minimal interruption of service\.   
 The following example illustrates a cluster endpoint for an Aurora MySQL DB cluster\.   
 `mydbcluster.cluster-123456789012.us-east-1.rds.amazonaws.com:3306` 

**Reader endpoint**  
 A *reader endpoint* for an Aurora DB cluster provides load\-balancing support for read\-only connections to the DB cluster\. Use the reader endpoint for read operations, such as queries\. By processing those statements on the read\-only Aurora Replicas, this endpoint reduces the overhead on the primary instance\. It also helps the cluster to scale the capacity to handle simultaneous `SELECT` queries, proportional to the number of Aurora Replicas in the cluster\. Each Aurora DB cluster has one reader endpoint\.   
 If the cluster contains one or more Aurora Replicas, the reader endpoint load\-balances each connection request among the Aurora Replicas\. In that case, you can only perform read\-only statements such as `SELECT` in that session\. If the cluster only contains a primary instance and no Aurora Replicas, the reader endpoint connects to the primary instance\. In that case, you can perform write operations through the endpoint\.   
 The following example illustrates a reader endpoint for an Aurora MySQL DB cluster\.   
 `mydbcluster.cluster-ro-123456789012.us-east-1.rds.amazonaws.com:3306` 

**Custom endpoint**  
 A *custom endpoint* for an Aurora cluster represents a set of DB instances that you choose\. When you connect to the endpoint, Aurora performs load balancing and chooses one of the instances in the group to handle the connection\. You define which instances this endpoint refers to, and you decide what purpose the endpoint serves\.   
 An Aurora DB cluster has no custom endpoints until you create one\. You can create up to five custom endpoints for each provisioned Aurora cluster\. You can't use custom endpoints for Aurora Serverless clusters\.   
 The custom endpoint provides load\-balanced database connections based on criteria other than the read\-only or read/write capability of the DB instances\. For example, you might define a custom endpoint to connect to instances that use a particular AWS instance class or a particular DB parameter group\. Then you might tell particular groups of users about this custom endpoint\. For example, you might direct internal users to low\-capacity instances for report generation or ad hoc \(one\-time\) querying, and direct production traffic to high\-capacity instances\.   
 Because the connection can go to any DB instance that is associated with the custom endpoint, we recommend that you make sure that all the DB instances within that group share some similar characteristic\. Doing so ensures that the performance, memory capacity, and so on, are consistent for everyone who connects to that endpoint\.   
 This feature is intended for advanced users with specialized kinds of workloads where it isn't practical to keep all the Aurora Replicas in the cluster identical\. With custom endpoints, you can predict the capacity of the DB instance used for each connection\. When you use custom endpoints, you typically don't use the reader endpoint for that cluster\.   
 The following example illustrates a custom endpoint for a DB instance in an Aurora MySQL DB cluster\.   
 `myendpoint.cluster-custom-123456789012.us-east-1.rds.amazonaws.com:3306` 

**Instance endpoint**  
 An *instance endpoint* connects to a specific DB instance within an Aurora cluster\. Each DB instance in a DB cluster has its own unique instance endpoint\. So there is one instance endpoint for the current primary DB instance of the DB cluster, and there is one instance endpoint for each of the Aurora Replicas in the DB cluster\.   
 The instance endpoint provides direct control over connections to the DB cluster, for scenarios where using the cluster endpoint or reader endpoint might not be appropriate\. For example, your client application might require more fine\-grained load balancing based on workload type\. In this case, you can configure multiple clients to connect to different Aurora Replicas in a DB cluster to distribute read workloads\. For an example that uses instance endpoints to improve connection speed after a failover for Aurora PostgreSQL, see [Fast failover with Amazon Aurora PostgreSQL](AuroraPostgreSQL.BestPractices.md#AuroraPostgreSQL.BestPractices.FastFailover)\. For an example that uses instance endpoints to improve connection speed after a failover for Aurora MySQL, see [MariaDB Connector/J failover support – case Amazon Aurora](https://mariadb.org/mariadb-connectorj-failover-support-case-amazon-aurora/)\.   
 The following example illustrates an instance endpoint for a DB instance in an Aurora MySQL DB cluster\.   
 `mydbinstance.123456789012.us-east-1.rds.amazonaws.com:3306` 
