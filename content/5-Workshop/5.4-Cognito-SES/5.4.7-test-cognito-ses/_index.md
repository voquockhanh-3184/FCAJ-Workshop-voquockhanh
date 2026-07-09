---
title : "Test Cognito and SES Integration"
date : 2024-01-01 
weight : 5
chapter : false
pre : " <b> 5.4.7. </b> "
---

#### Verification Steps:

1. In the Cognito User Pool console, navigate to the **App integration** tab -> Scroll down to the **App clients** section -> Click on the initialized App Client.
2. In the **Hosted UI** section, click **View login page** to launch the default Cognito authentication page.

![View Login Page](/images/5-Workshop/5.4-Cognito-SES/TestCognitoSES4.1.png)

3. Perform a test signup:
- Input the Email and Password details.
- *Note:* Due to the SES Sandbox state, you must register using email addresses that have already been verified in SES.
- Click **Sign up**.

![Hosted UI Sign up](/images/5-Workshop/5.4-Cognito-SES/TestCognitoSES4.2.png)

4. A verification email containing an OTP code will be dispatched from Amazon SES to the user's inbox. Check your mailbox -> Copy the verification code and enter it in the **Verification code** field on the Cognito Hosted UI page.

![Enter Verification Code](/images/5-Workshop/5.4-Cognito-SES/TestCognitoSES4.3.png)

5. Once verified, return to the Cognito Console:
- Click the **Users** tab inside your User Pool.
- Inspect the user directory. If the newly registered user displays a status of **Confirmed** in the **Confirmation status** column, it indicates the Cognito and SES integration is operating successfully.

![User Confirmed Status](/images/5-Workshop/5.4-Cognito-SES/TestCognitoSES4.4.png)
