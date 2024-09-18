---
title: Deployment Validation
parent: Quickstart
nav_order: 1
---
# InsuranceLake Deployment Validation

1. Transfer the sample claim data to the Collect bucket (Source system: SyntheticData, Table: ClaimData)
   ```bash
   aws s3 cp resources/syntheticgeneral-claim-data.csv s3://<Collect S3 Bucket>/SyntheticGeneralData/ClaimData/
   ```

1. Transfer the sample policy data to the Collect bucket (Source system: SyntheticData, Table: PolicyData)
   ```bash
   aws s3 cp resources/syntheticgeneral-policy-data.csv s3://<Collect S3 Bucket>/SyntheticGeneralData/PolicyData/
   ```

1. Upon successful load of file S3 event notification will trigger the state-machine-trigger Lambda function

1. This Lambda function will insert a record into the DynamoDB table `{environment}-{resource_name_prefix}-etl-job-audit` to track job start status

1. The Lambda function will also trigger the Step Functions State Machine. The State Machine execution name will be `<filename>-<YYYYMMDDHHMMSSxxxxxx>` and have the required metadata as input parameters

1. The State Machine will trigger the Glue job for Collect to Cleanse data processing

1. The Collect to Cleanse Glue job will execute the transformation logic defined in configuration files

1. Glue job will load the data into the Cleanse bucket using the provided metadata and data will be stored in S3 as `s3://{environment}-{resource_name_prefix}-{account}-{region}-cleanse/syntheticgeneraldata/claimdata/year=YYYY/month=MM/day=DD` in Apache Parquet format

1. Glue job will create/update the Glue Catalog table using the table name passed as parameter based on folder name (`PolicyData` and `ClaimData`)

1. After the Collect to Cleanse job completes, the State Machine will trigger the Cleanse to Consume Glue job

1. The Cleanse to Consume Glue job will execute the SQL logic defined in configuration files

1. The Cleanse to Consume Glue job will store the resulting data set in S3 as `s3://{environment}-{resource_name_prefix}-{account}-{region}-consume/syntheticgeneraldata/claimdata/year=YYYY/month=MM/day=DD` in Apache Parquet format

1. The Cleanse to Consume Glue job will create/update the Glue Catalog table

1. After successful completion of the Cleanse to Consume Glue job, the State Machine will trigger the etl-job-auditor Lambda function to update the DynamoDB table `{environment}-{resource_name_prefix}-etl-job-audit` with the latest status

1. An SNS notification will be sent to all subscribed users

1. To validate the data, use the Athena and execute the following query:

    ```sql
    select * from syntheticgeneraldata_consume.policydata limit 100
    ```