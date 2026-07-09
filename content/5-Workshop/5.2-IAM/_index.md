---
title : "IAM Setup for Examora"
date : 2024-01-01 
weight : 2 
chapter : false
pre : " <b> 5.2. </b> "
---

In this step, we will configure IAM to prepare the AWS account for the **Examora - Online Exam Platform** project.

#### 5.2.1. Objectives

**IAM** in Examora plays 2 main roles:

> **a. Human access**
> Developers log in to the AWS Console to initialize, manage, and verify resources.
>
> **b. Workload access**
> AWS Lambda, API Gateway, and other services use IAM Roles to securely communicate with and access AWS Secrets Manager, Amazon S3, Amazon SQS, and Amazon CloudWatch.

#### Content

1. [Create AWS Account Alias](5.2.2-create-account-alias/)
2. [Create IAM Admin Group](5.2.3-create-admin-group/)
3. [Create IAM User and Enable MFA](5.2.4-create-iam-user/)
4. [Attach IAM permission policy](5.2.5-attach-policy/)
