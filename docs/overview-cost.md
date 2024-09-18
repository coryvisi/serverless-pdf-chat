---
title: Cost
parent: Overview
---
## Cost

This solution uses the following services: [Amazon Simple Storage Service (S3)](https://aws.amazon.com/s3/pricing/), [AWS Glue](https://aws.amazon.com/glue/pricing/), [AWS Step Functions](https://aws.amazon.com/step-functions/pricing/), [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/pricing/), [Amazon Athena](https://aws.amazon.com/athena/pricing/), [AWS Cloud9](https://aws.amazon.com/cloud9/pricing/) (for recommended installation process only), [AWS CodePipeline](https://aws.amazon.com/codepipeline/pricing/) (for CI/CD installation only).

An estimated cost for following the [Quickstart](#quickstart) and [Quickstart with CI/CD](#quickstart-with-cicd) instructions, assuming a total of 8 Glue DPU hours and cleaning all resources when finished, **your cost will not be higher than $2**. This cost could be less as some services are included in the Free Tier.

_We recommend creating a [Budget](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html) through [AWS Cost Explorer](https://aws.amazon.com/aws-cost-management/aws-cost-explorer/) to help manage costs. Prices are subject to change. For full details, refer to the pricing webpage for each AWS service used in this solution._

### Sample Cost Table

The following table provides a sample cost breakdown for deploying this Guidance with the default parameters in the US East (Ohio) Region for one month with pricing as of _9 July 2024_.

|AWS service    |Dimensions |Cost [USD]
|---    |---    |---
|AWS Glue   |per DPU-Hour for each Apache Spark or Spark Streaming job, billed per second with a 1-minute minimum   |$0.44
|Amazon S3  |per GB of storage used, Frequent Access Tier, first 50 TB per month<br>PUT, COPY, POST, LIST requests (per 1,000 requests)<br>GET, SELECT, and all other requests (per 1,000 requests)   |$0.023<br>$0.005<br>$0.0004
|Amazon Athena  |per TB of data scanned   |$5.00
|Amazon DynamoDB    |per million Write Request Units (WRU)<br>per million Read Request Units (RRU)  |$1.25<br>$0.25
