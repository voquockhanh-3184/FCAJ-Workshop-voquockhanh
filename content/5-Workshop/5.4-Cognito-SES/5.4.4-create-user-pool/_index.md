---
title : "Create Cognito User Pool"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.4.4. </b> "
---

#### Concept:
An **Amazon Cognito User Pool** is a fully managed user directory that handles user authentication and authorization for web and mobile applications. It acts as an OpenID Connect (OIDC) identity provider and issues JWT tokens containing the authenticated user's identity claims.

#### Objective:
Create an **Amazon Cognito User Pool** to handle user signup, login, and authorization for Examora, and configure it to automatically dispatch verification emails via **Amazon SES**.

#### Configuration Steps:

1. Search for and select the **Cognito** service in the AWS Management Console.
- On the left sidebar menu, choose **User pools** -> Click **Create user pool**.

![Create User Pool](/images/5-Workshop/5.4-Cognito-SES/COGNITO4.1.png)

2. Configure User Pool properties:
- In the **Application type** section, select **Single-page application (SPA)**.
- Set the User Pool Name (e.g., `examora-user-pool`).
- Under **Configure options**, select the check box for **Email**.
- Enter your Frontend Local URL (this URL will be updated later once hosted via S3 + CloudFront).
- Click **Create user directory** to initialize.

![Configure SPA](/images/5-Workshop/5.4-Cognito-SES/COGNITO4.2.png)

![User Directory Info](/images/5-Workshop/5.4-Cognito-SES/COGNITO4.3.png)

3. Click on the newly created User Pool to retrieve the following critical configuration environment variables:
- `AWS_REGION = ap-southeast-1`
- `COGNITO_USER_POOL_ID = <your User Pool ID>`
- `COGNITO_APP_CLIENT_ID = <your Client ID>`
- `COGNITO_ISSUER_URL = https://cognito-idp.ap-southeast-1.amazonaws.com/<User Pool ID>`

4. Configure automatic email verification for user registration:
- In the **Attribute verification and user account confirmation** section -> Select **Allow Cognito to automatically send messages to verify and confirm** and choose **Send email message, verify email address**.
- This setup enables Cognito to automatically dispatch OTP codes to verify and confirm a user's account upon signup.

![Attribute Verification](/images/5-Workshop/5.4-Cognito-SES/COGNITO4.4.png)

5. Update the Verification message template so that the verification email matches the branding and style of the Examora project.

![Message Template](/images/5-Workshop/5.4-Cognito-SES/COGNITO4.5.png)
