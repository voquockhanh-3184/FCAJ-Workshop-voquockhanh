---
title : "Configure JWT Authorizer and CORS for API Gateway"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.6.3. </b> "
---

#### Objectives:
*   Configure a **JWT Authorizer** for API Gateway to validate API request credentials using tokens issued by Amazon Cognito. API Gateway will inspect, cryptographically verify, and decode the JWT before forwarding the request to the Lambda Backend API.
*   Configure **CORS** policies to allow the React Frontend running locally (`http://localhost:5173`) or in production to safely send cross-origin HTTP requests to API Gateway.

#### Step-by-Step Instructions:

1. Configure JWT Authorizer:
   * In the left panel under **Develop** -> select **Authorization** -> choose the **Manage authorizers** tab -> click **Create**.
   * Fill in the authorization parameters:
     * **Name**: `examora-cognito-jwt-authorizer-dev`
     * **Identity source**: `$request.header.Authorization` (specifies that API Gateway will look for the JWT token inside the `Authorization` request header).
     * **Issuer URL**: `https://cognito-idp.ap-southeast-1.amazonaws.com/<COGNITO_USER_POOL_ID>` (Replace `<COGNITO_USER_POOL_ID>` with your actual Cognito User Pool ID).
     * **Audience**: Enter your `<COGNITO_APP_CLIENT_ID>` (the Client ID generated in the Cognito setup).
   * Click **Create** to save the authorizer.

   ![Create JWT Authorizer](/images/5-Workshop/5.6-API-Gateway/5.6.3-configure-jwt-authorizer-cors/API6.8.png)

2. Attach the Authorizer to Examora Business Routes:
   * Navigate back to **Routes** -> select the `ANY /{proxy+}` route (which encompasses all private backend application endpoints).
   * Select **Attach authorization** -> choose the authorizer: `examora-cognito-jwt-authorizer-dev`.
   * Click **Attach authorizer** -> click **Save** to persist the configuration.
   * *Note*: Leave the `GET /health` route public (without an authorizer attached) to permit public monitoring.

   ![Attach Authorizer to Route](/images/5-Workshop/5.6-API-Gateway/5.6.3-configure-jwt-authorizer-cors/API6.9.png)

3. Configure CORS:
   * To allow the frontend to invoke the API Gateway from another origin/domain, CORS must be configured.
   * Go to the **CORS** tab in the left panel -> click **Configure** -> specify the permitted CORS headers, methods, and origins -> click **Save**.

   ![Configure CORS](/images/5-Workshop/5.6-API-Gateway/5.6.3-configure-jwt-authorizer-cors/CORS6.1.png)

> [!NOTE]
> Navigate back to your **Lambda Function** -> go to the **Configuration** tab -> select **Permissions** -> scroll down to the **Resource-based policy statements** section. Verify that a policy statement exists allowing API Gateway to invoke the Lambda function. This permissions policy is mandatory for API Gateway to invoke your Lambda backend.
>
> ![Resource-based Policy Statement](/images/5-Workshop/5.6-API-Gateway/5.6.3-configure-jwt-authorizer-cors/LambdaInvoke.png)
