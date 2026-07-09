---
title : "Configure Cognito User Pool + SES for Examora"
date : 2024-01-01 
weight : 4 
chapter : false
pre : " <b> 5.4. </b> "
---

In this step, we will configure **Amazon Cognito User Pool** combined with **Amazon SES** to handle user authentication and authorization for the **Examora - Online Exam Platform ** project.

#### 5.4.1. Objectives
The authentication system will manage the following key features:
*   User registration and login using Email/Password.
*   Automatic dispatch of verification codes via email upon registration.
*   Password recovery and reset flows (forgot/change password).
*   Issuance of JWT (JSON Web Tokens) claims upon successful authentication.
*   User categorization using Cognito Groups for role-based access control: **ADMIN**, **TEACHER**, **STUDENT**.

#### 5.4.2. Configuration Scope
The required resources and settings to configure include:
1.  **Amazon SES Verified Identity**: Verify the sender email address.
2.  **Cognito User Pool**: Set up the user directory.
3.  **Cognito App Client**: Configure the client application properties.
4.  **Cognito Groups**: Initialize the ADMIN, TEACHER, and STUDENT roles.
5.  **Cognito Email Integration**: Integrate Amazon SES as the email provider.
6.  **Verification**: Test user sign-up, OTP validation, and verify the user's Confirm status.

#### Content

1. [Configure Amazon SES for Cognito Emails](5.4.3-configure-ses/)
2. [Create Cognito User Pool for Examora](5.4.4-create-user-pool/)
3. [Create Cognito Groups for Examora](5.4.5-create-cognito-groups/)
4. [Configure Cognito Email using SES](5.4.6-configure-email-ses/)
5. [Test Cognito & SES Integration on Console](5.4.7-test-cognito-ses/)
