---
title : "Create HTTP API and Attach Lambda Backend"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.6.1. </b> "
---

#### Step-by-Step Instructions:

1. Create HTTP API:
   * Navigate to the **API Gateway** console -> choose **HTTP API** to start creating a new API.
   * Configure the API parameters:
     * **API name**: Enter a descriptive name (e.g., `examora-api`).
     * **IP address type**: Select `IPv4`.
     * **Integration**: Choose **Lambda**, then specify your **AWS Region** and the **Lambda function** created in the previous section (`examora-backend-api`).

   ![Configure API Integration](/images/5-Workshop/5.6-API-Gateway/5.6.1-create-http-api/API6.2.png)

2. Configure Routes for the Express Backend:
   * Create the following routes to map incoming requests to the Lambda backend function:
     * **Route 1**: Method `GET`, Path `/health` (used to verify public accessibility before configuring authentication filters).
     * **Route 2**: Method `ANY`, Path `/{proxy+}` (acts as a greedy path parameter proxy to forward all API routes like `/api/auth/me`, `/api/lop-hoc`, `/api/lich-su-thi` directly to the Express router).

   ![Configure API Routes](/images/5-Workshop/5.6-API-Gateway/5.6.1-create-http-api/API6.3.png)

3. Configure Stages and Finalize:
   * Click **Next** to proceed to the Configure stages step. Keep the default stage configuration (`$default`) as-is.
   * Click **Next** to perform a final review of the API configurations.

   ![Configure Stages](/images/5-Workshop/5.6-API-Gateway/5.6.1-create-http-api/API6.4.png)

   * Click **Create** and wait for the API creation confirmation message.

   ![API Created Successfully](/images/5-Workshop/5.6-API-Gateway/5.6.1-create-http-api/API6.5.png)
