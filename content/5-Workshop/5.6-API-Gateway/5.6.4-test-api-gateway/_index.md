---
title : "Verify API Gateway Functionality"
date : 2024-01-01 
weight : 4
chapter : false
pre : " <b> 5.6.4. </b> "
---

#### Test Case 1: Invoking `/api/auth/me` without an authentication token
*   **Expected Result**: API Gateway rejects the request, returning a `401 Unauthorized` HTTP status.
*   **Actual Result**:

   ![Test Case 1](/images/5-Workshop/5.6-API-Gateway/5.6.4-test-api-gateway/TestAPI1.png)

*   *Assessment*: The Cognito JWT Authorizer is correctly intercepting and blocking unauthenticated requests before they reach the Lambda backend execution context.

---

#### Test Case 2: Invoking `/api/auth/me` with a valid Cognito JWT
*   Navigate to the local frontend application, log in successfully via Amazon Cognito, and ensure a session token is active.
*   Open the browser Developer Tools (F12) -> navigate to the **Console** tab, and execute the following test script:

```javascript
fetch("https://4js2c8rp18.execute-api.ap-southeast-1.amazonaws.com/api/auth/me", {
  headers: {
    Authorization: `Bearer ${localStorage.getItem("token")}`
  }
})
  .then(async res => {
    console.log("status", res.status);
    console.log(await res.text());
  })
  .catch(console.error);
```

*   **Expected Result**: Returns the user profile JSON object retrieved from MongoDB Atlas.
*   **Actual Result**:

   ![Test Case 2](/images/5-Workshop/5.6-API-Gateway/5.6.4-test-api-gateway/TestAPI2.png)

*   *Assessment*: The output demonstrates that API Gateway successfully authorizes the request using the Cognito JWT credentials, routes the payload to the Lambda Backend API, which successfully accesses MongoDB Atlas to retrieve and return the user profile.
*   *Conclusion*: The end-to-end authentication and integration chain (**Cognito -> API Gateway JWT Authorizer -> Lambda Backend API -> MongoDB Atlas**) is fully functional.

Finally, update the API Gateway invoke endpoint URL in the frontend application environment variables to complete the backend integration.
