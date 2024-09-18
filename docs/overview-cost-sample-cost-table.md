---
title: Sample Cost Table
nav_order: 3
parent: Cost
---
### Sample Cost Table

The following table provides a sample cost breakdown for deploying this Guidance with the default parameters in the US East (Ohio) Region for one month with pricing as of _9 July 2024_.

|AWS service    |Dimensions |Cost [USD]
|---    |---    |---
|AWS Glue   |per DPU-Hour for each Apache Spark or Spark Streaming job, billed per second with a 1-minute minimum   |$0.44
|Amazon S3  |per GB of storage used, Frequent Access Tier, first 50 TB per month<br>PUT, COPY, POST, LIST requests (per 1,000 requests)<br>GET, SELECT, and all other requests (per 1,000 requests)   |$0.023<br>$0.005<br>$0.0004
|Amazon Athena  |per TB of data scanned   |$5.00
|Amazon DynamoDB    |per million Write Request Units (WRU)<br>per million Read Request Units (RRU)  |$1.25<br>$0.25
