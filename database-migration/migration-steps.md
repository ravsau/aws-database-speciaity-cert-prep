

## Step 1: Migration Assessment
During Migration Assessment, a team of system architects reviews the architecture of
the existing application, produces an assessment report that includes a network
diagram with all the application layers, identifies the application and database
components that are not automatically migrated, and estimates the effort for manual
conversion work. Although migration analysis tools exist to expedite the evaluation, the
bulk of the assessment is conducted by internal staff or with help from AWS
Professional Services. **This effort is usually 2% of the whole migration effort.**
One of the key tools in the assessment analysis is the Database Migration Assessment
Report. This report provides important information about the conversion of the schema
from your source database to your target RDS database instance.


## Step 2: Schema Conversion
The Schema Conversion step consists of translating the data definition language
(DDL) for tables, partitions, and other database storage objects from the syntax and
features of the source database to the syntax and features of the target database.
Schema conversion in the AWS SCT is a two-step process:
1. Convert the schema.
2. Apply the schema to the target database.
AWS SCT also converts procedural application code in triggers, stored procedures, and
functions from feature-rich languages (e.g., PLSQL, T-SQL) to the simpler procedural
languages of MySQL and PostgreSQL. **Schema conversion typically accounts for 30%
of the whole migration effort.**

The AWS SCT automatically creates DDL scripts for as many database objects on the
target platform as possible. For the remaining database objects, the conversion action
items describe why the object cannot be converted automatically and the manual steps
required to convert the object to the target platform.



## Step 3: Conversion of Embedded SQL and Application Code
After you convert the database schema, the next step is to address any custom scripts
with embedded SQL statements (e.g., ETL scripts, reports, etc.) and the application
code so that they work with the new target database. This includes rewriting portions of
application code written in Java, C#, C++, Perl, Python, etc., that relate to JDBC/ODBC
driver usage, establishing connections, data retrieval, and iteration. AWS SCT scans a
folder containing application code, extracts embedded SQL statements, converts as
many as possible automatically, and flags the remaining statements for manual

conversion actions.
**Converting embedded SQL in application code typically accounts
for 15% of the whole migration effort.
Some applications are more reliant on database objects, such as stored procedures,
while other applications use more embedded SQL for database queries. In either case,
these two efforts combined typically account for around 45%, or almost half, of the
migration effort.**


## Step 4: Data Migration
After the schema and application code are successfully converted to the target
database platform, it is time to migrate data from the source database to the target
database. You can easily accomplish this by using AWS DMS. After the data is
migrated, you can perform testing on the new schema and application. Because much
of the data mapping and transformation work has already been done in AWS SCT and
AWS DMS manages the complexities of the data migration for you, configuring a new
**Data Migration Service is typically 5% of the whole migration effort.**

## Step 5: Testing Converted Code
After schema and application code has been converted and the data successfully
migrated onto the AWS platform, thoroughly test the migrated application. The focus of
this testing is to ensure correct functional behavior on the new platform. **Although best
practices vary, it is generally accepted to aim for as much time in the testing phase as in
the development phase, which is about 45% of the overall migration effort.**

##Step 6: Data Replication
Although a one-time full load of existing data is relatively simple to set up and run, many
production applications with large database backends cannot tolerate a downtime
window long enough to migrate all the data in a full load. For these databases, *AWS
DMS can use a proprietary Change Data Capture (CDC) process to implement ongoing
replication from the source database to the target database.** AWS DMS manages and
monitors the ongoing replication process with minimal load on the source database,
without platform-specific technologies and without components that need to be installed
on either the source or target. **Due to CDC’s ease-of-use, setting up data replication
typically accounts for 3% of the overall effort.**


## Step 7: Deployment to AWS and Go Live
Test the data migration of the production database to ensure that all data can be
successfully migrated during the allocated cutover window. Monitor the source and
target databases to ensure that the initial data load is completed, cached transactions
are applied, and data has reached a steady state before cutover. You can also use the
Enable Validation option available in the Task settings pane of AWS DMS (Figure 8).
If you select this option, AWS DMS validates the data migration by comparing the data
in the source and the target databases
Design a simple rollback plan for the unlikely event that an unrecoverable error occurs
during the Go Live window. The AWS SCT and AWS DMS work together to preserve
the original source database and application, so the rollback plan will mainly consist of
scripts to point connection strings back to the original source database.
