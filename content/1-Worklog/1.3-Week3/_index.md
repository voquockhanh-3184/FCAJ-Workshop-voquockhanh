---
title: "Worklog Week 3"
date: 2026-05-08
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

## FCAJ WORKLOG - WEEK 03: AUTHENTICATION & IDENTITY MANAGEMENT

**Performed by:** Vo Quoc Khanh  
**Group:** KQPSV Group  

---

### Week 3 Objectives:

* Research and implement a user identity management (Authentication) system on AWS.
* Integrate Amazon Cognito to provide:
  * Account registration.
  * User sign-in.
  * User Identity management.
  * JWT authentication token issuance.
* Set up security for the Serverless API by connecting Amazon Cognito with Amazon API Gateway.
* Complete the Frontend-Backend connection through the user authentication mechanism.

---

### Tasks to be implemented during this week:

| Day | Tasks | Start Date | Completion Date | Reference (Cloud Journey) |
| :--- | :--- | :--- | :--- | :--- |
| **Day 2** | - Learn about Amazon Cognito:<br>&emsp;+ User Pool<br>&emsp;+ Identity Pool<br>&emsp;+ Authentication Flow<br>&emsp;+ JWT Token | 04/05/2026 | 04/05/2026 | [User Authentication with Amazon Cognito](https://000081.awsstudygroup.com/) |
| **Day 3** | - **Hands-on:**<br>&emsp;+ Create a Cognito User Pool<br>&emsp;+ Configure sign-in with Email<br>&emsp;+ Create an App Client for a Single-page Application (SPA)<br>&emsp;+ Configure Cognito Hosted UI | 05/05/2026 | 05/05/2026 | [Single Page Application Authentication](https://000055.awsstudygroup.com) |
| **Day 4** | - **Hands-on:**<br>&emsp;+ Create an Identity Pool<br>&emsp;+ Configure the IAM Role for authenticated users<br>&emsp;+ Set up the Authenticated Role to prepare AWS resource authorization | 06/05/2026 | 06/05/2026 | [Cross-Domain Authentication with Amazon Cognito](https://000141.awsstudygroup.com) |
| **Day 5** | - Secure API Gateway with a Cognito Authorizer:<br>&emsp;+ Create a JWT Authorizer<br>&emsp;+ Configure the Issuer URL from the Cognito User Pool<br>&emsp;+ Verify the Audience using the App Client ID<br>&emsp;+ Apply the Authorizer to an API route | 07/05/2026 | 07/05/2026 | [Frontend Integration with API Gateway](https://000135.awsstudygroup.com/) |
| **Day 6** | - **Frontend integration hands-on:**<br>&emsp;+ Configure the OAuth 2.0 Flow<br>&emsp;+ Test sign-up/sign-in through the Hosted UI<br>&emsp;+ Retrieve the JWT ID Token<br>&emsp;+ Prepare to send the token via the Authorization header when calling the API | 08/05/2026 | 08/05/2026 | [Serverless Storage and Auth with AWS Amplify](https://000134.awsstudygroup.com/) |

---

### Week 3 Achievements:

* Understood the Authentication and Authorization mechanism in a Serverless system using AWS Cognito.

* Successfully configured Amazon Cognito:
  * Created a User Pool to manage user accounts.
  * Configured Email-based authentication.
  * Created an App Client for a Single-page Application (SPA).
  * Set up the Cognito Hosted UI for sign-up and sign-in.

* Successfully created an Identity Pool:
  * Connected it to the User Pool.
  * Configured the IAM Role for authenticated users.
  * Prepared the mechanism for AWS resource access authorization.

* Successfully secured API Gateway with a Cognito JWT Authorizer:
  * Created an Authorizer on the HTTP API Gateway.
  * Configured the Issuer URL linked to the Cognito User Pool.
  * Verified the Audience via the App Client ID.
  * Applied authentication to API Routes such as `POST /users`.

* Successfully integrated the authentication flow between Frontend and Backend:
  * Signed up and signed in through the Cognito Hosted UI.
  * Retrieved the JWT ID Token after authentication.
  * Prepared the token to be sent in the `Authorization` Header when calling the API.

---

### Blockers & Solutions:

* **Issue:** Could not directly retrieve the JWT ID Token after signing in through the Cognito Hosted UI.

* **Root Cause:**
  * The Cognito App Client defaults to the OAuth 2.0 Authorization Code Grant.
  * After a successful sign-in, the browser only returns an Authorization Code in the form: