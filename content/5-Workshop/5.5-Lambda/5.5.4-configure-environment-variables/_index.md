---
title : "Configure Environment Variables and X-Ray Tracing"
date : 2024-01-01 
weight : 4
chapter : false
pre : " <b> 5.5.4. </b> "
---

We need to configure environment variables for the Lambda function so that the Express backend can load the necessary runtime environment configurations (e.g., Cognito settings for JWT verification, allowed origins for CORS, and the Secrets Manager path via `MONGO_SECRET_NAME` to pull database credentials). We will also enable AWS X-Ray to trace and diagnose requests.

#### Step-by-Step Instructions:

1. Select the newly created function -> navigate to the **Configuration** tab -> choose **Environment variables** -> click **Edit** -> Populate the key-value pairs required for the project -> click **Save** to apply the configuration.

   ![Configure Environment Variables](/images/5-Workshop/5.5-Lambda/5.5.4-configure-environment-variables/LambdaEnv5.1.png)

2. Enable AWS X-Ray Tracing:
   * AWS X-Ray provides end-to-end tracing, allowing you to monitor request paths and latency profiles as events travel from API Gateway through Lambda to the database, making it easy to debug performance bottlenecks or runtime errors.
   * Under the **Configuration** tab -> select **Monitoring and operations tools** in the left panel -> click **Edit** in the top right.
   * In the **CloudWatch Application Signals and AWS X-Ray** section -> check the **Enable** option for **Lambda service traces**.
   * Click **Save** to apply the configuration.

   ![Enable AWS X-Ray Tracing](/images/5-Workshop/5.5-Lambda/5.5.4-configure-environment-variables/LambdaXRay5.1.png)
