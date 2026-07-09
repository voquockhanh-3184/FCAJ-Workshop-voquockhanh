---
title : "Configure AWS Secrets Manager for Examora"
date : 2024-01-01 
weight : 3 
chapter : false
pre : " <b> 5.3. </b> "
---

In this step, we will configure AWS Secrets Manager to securely store the MongoDB Atlas database connection details for the Examora project.

#### 5.3.1. Objectives and Prerequisites

*   **AWS Secrets Manager** is used to securely store, manage, and retrieve credentials, API keys, and other secrets. The service supports encryption, detailed access control, automatic rotation, and usage auditing.
*   In this section, we will create a secret in AWS Secrets Manager to store the MongoDB Atlas connection string for the Examora project.
*   This secret enables the Lambda backend to dynamically read the database configuration without hardcoding the connection string in the source code or `.env` files.

**Prerequisites before creating the secret:**
1.  A MongoDB Atlas connection string in the following format:
    `mongodb+srv://<username>:<password>@<cluster-url>/<DBName>?retryWrites=true&w=majority`
2.  Database name: **WebsiteTest2026**
3.  AWS Region: **ap-southeast-1**
4.  An IAM user with permissions to create and manage Secrets Manager secrets.

#### Content

1. [Create secret in AWS Secrets Manager](5.3.2-create-secret/)
