- To monitor database activity with Amazon Aurora, you can use the Database Activity Streams feature. Database activity streams provide a near real-time data stream of the database activity in your relational database. When you integrate database activity streams with monitoring tools, you can monitor and audit database activity.

- Beyond external security threats, managed databases need to provide protection against insider risks from database administrators (DBAs). Database activity streams help protect your databases from internal threats by controlling DBA access to the database activity streams. Thus, the collection, transmission, storage, and subsequent processing of the stream of database activity is beyond the access of the DBAs that manage the database.

- A stream of database activity is pushed from Aurora to an Amazon Kinesis data stream that is created on behalf of your Aurora DB cluster. From Kinesis, the activity stream can then be consumed by AWS services such as Amazon Kinesis Data Firehose and AWS Lambda, or by applications for compliance management. For database activity streams with Aurora PostgreSQL, these compliance applications include IBM's Security Guardium, McAfee's Data Center Security Suite, and Imperva's SecureSphere Database Audit and Protection. Such applications can use the activity stream information to generate alerts and provide auditing of all activity on your Aurora DB clusters.



- Activity streams work for both mysql and Aurora with a few conditions


- https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/DBActivityStreams.html
