
- https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Managing.Clone.html

- Using the Aurora cloning feature, you can quickly and cost-effectively create a new cluster containing a duplicate of an Aurora cluster volume and all its data. We refer to the new cluster and its associated cluster volume as a clone.
  - Creating a clone is faster and more space-efficient than physically copying the data using a different technique such as restoring a snapshot.
  
### Use Cases: 
You can use cloning in a variety of use cases, especially where you don't want to have an impact on your production environment. Some examples are the following:

- Experiment with and assess the impact of changes, such as schema changes or parameter group changes.

- Perform workload-intensive operations, such as exporting data or running analytical queries.

- Create a copy of a production DB cluster in a nonproduction environment for development or testing.


#### Limitations
- Can only be done on the same region 



### How to do it Across Accounts ? 
- You can now share your Amazon Aurora DB clusters with other AWS accounts for quick and efficient database cloning.
