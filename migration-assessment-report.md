## What does a report look like ? 

![image](https://user-images.githubusercontent.com/22568316/103101449-adc30a80-45e5-11eb-823c-dda8d3507265.png)

https://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_AssessmentReport.Summary.html


## What does it contain? 
The migration assessment report includes the following:

- Executive summary

- License evaluation

- Cloud support, indicating any features in the source database not available on the target.

- Current source hardware configuration

- Recommendations, including conversion of server objects, backup suggestions, and linked server changes

The report includes information about an Amazon RDS DB instance if you selected Amazon RDS as your target, including the following:

    - The currently used storage size and maximum storage size for the DB instance.

    - The current number of databases on the DB instance and the maximum number of databases allowed on the DB instance.

    - A list of database services and server objects that are not available on the DB instance.

    - A list of databases that are currently participating in replication. Amazon RDS doesn't support replication.

    - The report also includes estimates of the amount of effort that it will take to write the equivalent code for your target DB instance that can't be converted automatically. This Estimated Complexity field is exported in the PDF version of the assessment report, but it's not included in the CSV version.

    - If you use AWS SCT to migrate your existing schema to an Amazon RDS DB instance, the report can help you analyze requirements for moving to the AWS Cloud and for changing your license type.
    - Link: https://docs.aws.amazon.com/SchemaConversionTool/latest/userguide/CHAP_AssessmentReport.html
