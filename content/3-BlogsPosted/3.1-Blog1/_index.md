---
title: "Blog 1"
date: 2026-07-05
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
# Automating Data Refresh Between AWS Accounts for Amazon RDS Multi-AZ DB Cluster

Automating data refresh between AWS accounts for Amazon RDS Multi-AZ DB Cluster helps synchronize production data to staging or testing environments without manual intervention. The solution uses a serverless architecture combining multiple AWS services to automate the entire process, while ensuring security when data is shared between accounts.

Key points to note:

* Amazon RDS does not support direct sharing of cluster snapshots of Multi-AZ DB Clusters between AWS accounts, so an intermediary process is required.
* The solution is implemented by:
Creating a cluster snapshot from the Multi-AZ DB Cluster.
Restoring the snapshot to a temporary Single-AZ DB Instance.
Create a DB instance snapshot from this instance.
Share the snapshot to the destination account and restore it to a new database.
* The entire process is automated using a serverless architecture, requiring no management server.
* AWS Lambda performs tasks such as snapshot creation, database restoration, snapshot sharing, and temporary resource cleanup.
* AWS Step Functions orchestrates the entire multi-step workflow, monitoring the status of RDS tasks and only moving to the next step when the previous one is complete.
* Amazon EventBridge transmits events between the source and destination accounts, automatically triggering subsequent steps without manual intervention.
* Data is protected by AWS KMS with a customer-managed KMS key, ensuring snapshots remain encrypted throughout the sharing process between accounts.
* When the snapshot is copied to the destination account, the data will be decrypted using the source account's KMS key and re-encrypted using the destination account's KMS key, meeting security requirements and separating key management rights.
* This solution is suitable for businesses deploying multi-account models on AWS, enabling fast data synchronization, increased operational efficiency, and enhanced security.

![Picture blog 1](/images/blog1.png)

[Link blog](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2200228570742103/#)

![Instruction](/images/instructionblog1.png)