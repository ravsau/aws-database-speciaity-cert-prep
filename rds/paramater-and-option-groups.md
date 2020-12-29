## Notes



## What is Parameter Groups in RDS?

A DB parameter group acts as a container for engine configuration values that are applied to one or more DB instances.


---
- When you change a dynamic parameter and save the DB parameter group, the change is applied immediately regardless of the Apply Immediately setting. When you change a static parameter and save the DB parameter group, the parameter change takes effect after you manually reboot the DB instance.

- You cannot modify the default Parameter groups or the default Option Groups
- By default RDS Creates a Parameter group when you create an RDS instance






---
## Options for SQL Server Option Group

- Native backup export to S3
- SQL Server Audit
- SQL Server Analysis Service
- SQL Server Reporting Service
- etc

https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Appendix.SQLServer.Options.html

----
