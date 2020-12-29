You can also restore your DynamoDB table data across AWS Regions such that the restored table is created in a different Region from where the backup resides. You can do cross-Region restores between AWS commercial Regions, AWS China Regions, and AWS GovCloud (US) Regions. You pay only for the data that you transfer out of the source Region and for restoring to a new table in the destination Region.

Restores can be faster and more cost-efficient if you choose to exclude some or all secondary indexes from being created on the new restored table.

You must manually set up the following on the restored table:

Auto scaling policies

AWS Identity and Access Management (IAM) policies

Amazon CloudWatch metrics and alarms

Tags

Stream settings

Time to Live (TTL) settings

You can only restore the entire table data to a new table from a backup. You can write to the restored table only after it becomes active.


- https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/backuprestore_HowItWorks.html

----

- You can restore a DynamoDB table to another Region
  - https://aws.amazon.com/blogs/database/restore-amazon-dynamodb-backups-to-different-aws-regions-and-with-custom-table-settings/
  
