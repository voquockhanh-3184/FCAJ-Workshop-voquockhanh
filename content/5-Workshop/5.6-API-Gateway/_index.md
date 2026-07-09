---
title : "Create API Gateway for Lambda Backend API"
date : 2024-01-01 
weight : 6 
chapter : false
pre : " <b> 5.6. </b> "
---

#### Objectives:

We will create a public API endpoint to expose the backend services to the frontend. API Gateway will validate JWT tokens issued by Amazon Cognito using a JWT Authorizer, and then route authorized requests to the Lambda function (Backend API).

API Gateway serves the following purposes:
*   Receives incoming HTTP requests from the frontend.
*   Validates JWT access tokens issued by Amazon Cognito User Pool.
*   Rejects unauthorized or malformed requests before they reach the Lambda runtime.
*   Routes authorized requests to the Lambda Backend API.
*   Configures CORS rules to allow secure requests from local or production frontend applications.

Upon completing this section, the frontend can invoke the backend using the following URL structure:
`https://<api-id>.execute-api.ap-southeast-1.amazonaws.com`

#### Sections:
1. [Create HTTP API and Attach Lambda Backend](5.6.1-create-http-api/)
2. [Test API Gateway Invoke URLs](5.6.2-test-invoke-url/)
3. [Configure JWT Authorizer and CORS for API Gateway](5.6.3-configure-jwt-authorizer-cors/)
4. [Verify API Gateway Functionality](5.6.4-test-api-gateway/)
