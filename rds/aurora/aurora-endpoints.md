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


------


## Membership rules for custom endpoints
When you add a DB instance to a custom endpoint or remove it from a custom endpoint, any existing connections to that DB instance remain active.

You can define a list of DB instances to include in, or exclude from, a custom endpoint. We refer to these lists as static and exclusion lists, respectively. You can use the inclusion/exclusion mechanism to further subdivide the groups of DB instances, and to make sure that the set of custom endpoints covers all the DB instances in the cluster. Each custom endpoint can contain only one of these list types.

In the AWS Management Console, the choice is represented by the check box Attach future instances added to this cluster. When you keep check box clear, the custom endpoint uses a static list containing only the DB instances specified in the dialog. When you choose the check box, the custom endpoint uses an exclusion list. In this case, the custom endpoint represents all DB instances in the cluster (including any that you add in the future) except the ones left unselected in the dialog. The AWS CLI and Amazon RDS API have parameters representing each kind of list. When you use the AWS CLI or Amazon RDS API, you can't add or remove individual members to the lists; you always specify the entire new list.

Aurora doesn't change the DB instances specified in the static or exclusion lists when DB instances change roles between primary instance and Aurora Replica due to failover or promotion. For example, a custom endpoint with type READER might include a DB instance that was an Aurora Replica and then was promoted to a primary instance. The type of a custom endpoint (READER, WRITER, or ANY) determines what kinds of operations you can perform through that endpoint.

You can associate a DB instance with more than one custom endpoint. For example, suppose that you add a new DB instance to a cluster, or that Aurora adds a DB instance automatically through the autoscaling mechanism. In these cases, the DB instance is added to all custom endpoints for which it is eligible. Which endpoints the DB instance is added to is based on the custom endpoint type of READER , WRITER, or ANY, plus any static or exclusion lists defined for each endpoint. For example, if the endpoint includes a static list of DB instances, newly added Aurora Replicas aren't added to that endpoint. Conversely, if the endpoint has an exclusion list, newly added Aurora Replicas are added to the endpoint, if they aren't named in the exclusion list and their roles match the type of the custom endpoint.

If an Aurora Replica becomes unavailable, it remains associated with any custom endpoints. For example, it remains part of the custom endpoint when it is unhealthy, stopped, rebooting, and so on. However, you can't connect to it through those endpoints until it becomes available again.

