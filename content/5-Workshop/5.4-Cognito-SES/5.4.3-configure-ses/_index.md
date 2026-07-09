---
title : "Configure Amazon SES for Cognito Emails"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.4.3. </b> "
---

#### Configuration Steps:

1. Log in to the AWS Management Console and ensure you select the correct region: **Singapore (ap-southeast-1)**.
2. In the AWS search bar, type **Amazon SES** -> Select **Amazon Simple Email Service** -> Navigate to **Identities** under the Configuration section on the left sidebar.

![Amazon SES Identities](/images/5-Workshop/5.4-Cognito-SES/SES4.1.png)

3. Create a sender email identity:
- Click the **Create identity** button.

![Create Identity](/images/5-Workshop/5.4-Cognito-SES/SES4.2.png)

- Under **Identity details**, select **Email address** as the **Identity type**.
- Enter the email address you wish to use as the sender address for Examora.
- Click **Create identity** at the bottom.

![Email Details](/images/5-Workshop/5.4-Cognito-SES/SES4.3.png)

- Open the inbox of the registered email address. Find and click the verification link sent by AWS to verify the email address identity.

![Email Verification Verification](/images/5-Workshop/5.4-Cognito-SES/SES4.4.png)

- Once verified, the identity status on the AWS Console will transition to **Verified**. This confirms the sender email address is verified successfully.

![SES Identity Verified](/images/5-Workshop/5.4-Cognito-SES/SES4.5.png)

#### Conclusion:
*   We have successfully configured **Amazon SES** in the `ap-southeast-1` region and verified the sender email identity for Examora. This email identity will be used within the Cognito User Pool configuration to dispatch verification codes and password recovery codes to users.
*   By default, new SES accounts reside in the **Sandbox environment**, meaning emails can only be sent to verified email addresses or domains. Therefore, for testing purposes, we must separately verify the test email addresses used for the ADMIN, TEACHER, and STUDENT accounts. To transition to a production environment later, you must request **SES Production Access** to dispatch emails to unverified recipients.
