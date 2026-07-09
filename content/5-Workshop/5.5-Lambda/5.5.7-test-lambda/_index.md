---
title : "Test Lambda Directly Before Attaching API Gateway"
date : 2024-01-01 
weight : 7
chapter : false
pre : " <b> 5.5.7. </b> "
---

Before configuring Amazon API Gateway to routing internet traffic, we can test the backend execution flow directly on the AWS Lambda Console by simulating an API Gateway HTTP API proxy event.

#### Step-by-Step Instructions:

1. Create a Simulated Test Event:
   * On the `examora-backend-api` function detail page -> click the **Test** tab.
   * Configure a new test event:
     * **Test event action**: Select **Create new event**.
     * **Event name**: Enter a name (e.g., `TestHealthGet`).
     * **Template**: Keep the default `hello-world` or select `apigateway-aws-proxy`.
     * **Event JSON**: Copy and paste the following mock API Gateway HTTP API payload v2 JSON:

   ```json
   {
     "version": "2.0",
     "routeKey": "GET /health",
     "rawPath": "/health",
     "rawQueryString": "",
     "headers": {
       "host": "example.com",
       "user-agent": "lambda-test"
     },
     "requestContext": {
       "http": {
         "method": "GET",
         "path": "/health"
       }
     },
     "isBase64Encoded": false
   }
   ```

   ![Create Test Event](/images/5-Workshop/5.5-Lambda/5.5.6-deploy-backend/LambdaNen5.3.png)

2. Run the Test:
   * Click the **Test** button in the upper right.
   * In the **Execution result** panel, verify the output response:
     * If the **statusCode** returned is **`200`** and the response body matches your Express `/health` routing response (e.g., `{"status":"OK"}`), the Express backend has successfully initialized and executed within the Lambda runtime.

   ![Successful Test Execution](/images/5-Workshop/5.5-Lambda/5.5.6-deploy-backend/LambdaNen5.4.png)

3. Review Execution Logs in Amazon CloudWatch:
   * AWS Lambda automatically forwards runtime logs to Amazon CloudWatch Logs.
   * Select the **Monitor** tab on the Lambda console -> click **View CloudWatch logs**.
   * On the CloudWatch Logs page, open the latest **Log Stream** to inspect connection attempts to MongoDB Atlas, runtime bootstrap warnings, memory consumption metrics, and the unique AWS Request ID.

   ![Check CloudWatch Logs](/images/5-Workshop/5.5-Lambda/5.5.6-deploy-backend/CloudWatchLog.png)

   * **CloudWatch Logs** are vital for debugging serverless architectures, verifying database handshakes, and monitoring resource allocation parameters (e.g., ensuring actual memory usage fits within configured bounds).

#### Summary:
We have successfully deployed the Express backend of Examora on **AWS Lambda** (Backend API), verified database connectivity, and ensured that request routing works seamlessly on the serverless compute plane.
