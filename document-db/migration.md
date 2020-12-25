## Migration Approaches
There are three primary approaches for migrating your data to Amazon DocumentDB.

Doc: https://docs.aws.amazon.com/documentdb/latest/developerguide/docdb-migration.html#docdb-migration-approaches

### Offline
The offline approach uses the mongodump and mongorestore tools to migrate your data from your source MongoDB deployment to your Amazon DocumentDB cluster. The offline method is the simplest migration approach, but it also incurs the most downtime for your cluster.

The basic process for offline migration is as follows:

Quiesce writes to your MongoDB source.

Dump collection data and indexes from the source MongoDB deployment.

Restore indexes to the Amazon DocumentDB cluster.

Restore collection data to the Amazon DocumentDB cluster.

Change your application endpoint to write to the Amazon DocumentDB cluster.


### Online

The online approach uses AWS Database Migration Service (AWS DMS). It performs a full load of data from your source MongoDB deployment to your Amazon DocumentDB cluster. It then switches to change data capture (CDC) mode to replicate changes. The online approach minimizes downtime for your cluster, but it is the slowest of the three methods.

The basic process for online migration is as follows:

Your application uses the source DB normally.

Optionally, pre-create indexes in the Amazon DocumentDB cluster.

Create an AWS DMS task to perform a full load, and then enable CDC from the source MongoDB deployment to the Amazon DocumentDB cluster.

After the AWS DMS task has completed a full load and is replicating changes to the Amazon DocumentDB, switch the application's endpoint to the Amazon DocumentDB cluster.


### Hybrid
The hybrid approach uses the mongodump and mongorestore tools to migrate your data from your source MongoDB deployment to your Amazon DocumentDB cluster. It then uses AWS DMS in CDC mode to replicate changes. The hybrid approach balances migration speed and downtime, but it is the most complex of the three approaches.

The basic process for hybrid migration is as follows:

Your application uses the source MongoDB deployment normally.

Dump collection data and indexes from the source MongoDB deployment.

Restore indexes to the Amazon DocumentDB cluster.

Restore collection data to the Amazon DocumentDB cluster.

Create an AWS DMS task to enable CDC from the source MongoDB deployment to the Amazon DocumentDB cluster.

When the AWS DMS task is replicating changes within an acceptable window, change your application endpoint to write to the Amazon DocumentDB cluster.
