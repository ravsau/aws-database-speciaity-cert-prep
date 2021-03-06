https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/SecondaryIndexes.html
****  


DynamoDB supports two types of secondary indexes:
+ **[Global secondary index](GSI.html) — **An index with a partition key and a sort key that can be different from those on the base table\. A global secondary index is considered "global" because queries on the index can span all of the data in the base table, across all partitions\. A global secondary index is stored in its own partition space away from the base table and scales separately from the base table\.
+ **[Local secondary index](LSI.html) — **An index that has the same partition key as the base table, but a different sort key\. A local secondary index is "local" in the sense that every partition of a local secondary index is scoped to a base table partition that has the same partition key value\.

You should consider your application's requirements when you determine which type of index to use\. The following table shows the main differences between a global secondary index and a local secondary index\.


For maximum query flexibility, you can create up to 20 global secondary indexes \(default quota\) and up to 5 local secondary indexes per table\. 
| Characteristic | Global Secondary Index | Local Secondary Index | 
| --- | --- | --- | 
| Key Schema | The primary key of a global secondary index can be either simple \(partition key\) or composite \(partition key and sort key\)\. | The primary key of a local secondary index must be composite \(partition key and sort key\)\. | 
| Key Attributes | The index partition key and sort key \(if present\) can be any base table attributes of type string, number, or binary\. | The partition key of the index is the same attribute as the partition key of the base table\. The sort key can be any base table attribute of type string, number, or binary\. | 
| Size Restrictions Per Partition Key Value | There are no size restrictions for global secondary indexes\. | For each partition key value, the total size of all indexed items must be 10 GB or less\. | 
| Online Index Operations | Global secondary indexes can be created at the same time that you create a table\. You can also add a new global secondary index to an existing table, or delete an existing global secondary index\. For more information, see [Managing Global Secondary Indexes](GSI.OnlineOps.md)\.  | Local secondary indexes are created at the same time that you create a table\. You cannot add a local secondary index to an existing table, nor can you delete any local secondary indexes that currently exist\. | 
| Queries and Partitions | A global secondary index lets you query over the entire table, across all partitions\.  | A local secondary index lets you query over a single partition, as specified by the partition key value in the query\. | 
| Read Consistency | Queries on global secondary indexes support eventual consistency only\. | When you query a local secondary index, you can choose either eventual consistency or strong consistency\. | 
| Provisioned Throughput Consumption | Every global secondary index has its own provisioned throughput settings for read and write activity\. Queries or scans on a global secondary index consume capacity units from the index, not from the base table\. The same holds true for global secondary index updates due to table writes\. | Queries or scans on a local secondary index consume read capacity units from the base table\. When you write to a table, its local secondary indexes are also updated; these updates consume write capacity units from the base table\. | 
| Projected Attributes | With global secondary index queries or scans, you can only request the attributes that are projected into the index\. DynamoDB does not fetch any attributes from the table\. | If you query or scan a local secondary index, you can request attributes that are not projected in to the index\. DynamoDB automatically fetches those attributes from the table\. | 
