---
title: Cleanup
parent: Quickstart
nav_order: 3
---
# Clean-up Instructions

## Contents

* [Clean-up Workflow-created Resources](#clean-up-workflow-created-resources)
* [Clean-up ETL Stacks](#clean-up-etl-stacks)
* [Clean-up Infrastructure Stacks](#clean-up-infrastructure-stacks)
* [Clean-up CDK Bootstrap](#clean-up-cdk-bootstrap-optional)

## Clean-up Workflow-created Resources

1. Use the `etl_cleanup.py` script to clear the S3 buckets, Glue Data Catalog entries, logs, and DynamoDB tables:
   ```bash
   AWS_DEFAULT_REGION=us-east-2 resources/etl_cleanup.py --mode allbuckets
   ```

   You can also manually empty all six InsuranceLake S3 buckets (cleanse, collect, consume, etl-scripts, glue_temp, access-logs) before cleaning up the stacks (below).

   **Important:** If you want to retain Glue Data Catalog entries, logs, and S3 bucket contents, **do not run the script above**. Follow the instructions below to remove all stack-created resources except the S3 buckets (which will fail due to them containing objects). The buckets follow the defined retention policy in [s3_bucket_zones_stack.py](https://github.com/aws-samples/aws-insurancelake-infrastructure/blob/main/lib/s3_bucket_zones_stack.py#L45).

## Clean-up ETL Stacks

1. Delete stacks using the command `cdk destroy --all`. When you see the following text, enter **y**, and press enter/return.

   ```bash
   Are you sure you want to delete: Test-InsuranceLakeEtlPipeline, Prod-InsuranceLakeEtlPipeline, Dev-InsuranceLakeEtlPipeline (y/n)?
   ```

   **Note:** This operation deletes the pipeline stacks only in the central deployment account

1. To delete stacks in **development** account, log onto Dev account, go to AWS CloudFormation console and delete the following stacks in the order listed:

   **Note:** For each environment below, be sure to delete the stacks in the order they are listed, so that stack dependencies do not prevent deletion

   1. Dev-InsuranceLakeEtlAthenaHelper
   1. Dev-InsuranceLakeEtlStepFunctions
   1. Dev-InsuranceLakeEtlGlue
   1. Dev-InsuranceLakeEtlDynamoDb

1. To delete stacks in **test** account, log onto Dev account, go to AWS CloudFormation console and delete the following stacks in the order listed:

   1. Test-InsuranceLakeEtlAthenaHelper
   1. Test-InsuranceLakeEtlStepFunctions
   1. Test-InsuranceLakeEtlGlue
   1. Test-InsuranceLakeEtlDynamoDb

1. To delete stacks in **prod** account, log onto Dev account, go to AWS CloudFormation console and delete the following stacks in the order listed:

   1. Prod-InsuranceLakeEtlAthenaHelper
   1. Prod-InsuranceLakeEtlStepFunctions
   1. Prod-InsuranceLakeEtlGlue
   1. Prod-InsuranceLakeEtlDynamoDb

## Clean-up Infrastructure Stacks

1. Delete stacks using the command `cdk destroy --all`. When you see the following text, enter **y**, and press enter/return.

   ```bash
   Are you sure you want to delete: Test-InsuranceLakeInfrastructurePipeline, Prod-InsuranceLakeInfrastructurePipeline, Dev-InsuranceLakeInfrastructurePipeline (y/n)?
   ```

   Note: This operation deletes the pipeline stacks only in the central deployment account

1. To delete stacks in **development** account, log onto the Dev account, go to AWS CloudFormation console and delete the following stacks:

   1. Dev-InsuranceLakeInfrastructureVpc
   1. Dev-InsuranceLakeInfrastructureS3BucketZones

1. To delete stacks in **test** account, log onto Dev account, go to AWS CloudFormation console and delete the following stacks:

   1. Test-InsuranceLakeInfrastructureVpc
   1. Test-InsuranceLakeInfrastructureS3BucketZones

1. To delete stacks in **prod** account, log onto Dev account, go to AWS CloudFormation console and delete the following stacks:

   1. Prod-InsuranceLakeInfrastructureVpc
   1. Prod-InsuranceLakeInfrastructureS3BucketZones

## Clean-up CDK Bootstrap (optional)

If you are not using AWS CDK for other purposes, you can also remove `CDKToolkit` stack in each target account. For more details refer to [AWS CDK Toolkit](https://docs.aws.amazon.com/cdk/latest/guide/cli.html)