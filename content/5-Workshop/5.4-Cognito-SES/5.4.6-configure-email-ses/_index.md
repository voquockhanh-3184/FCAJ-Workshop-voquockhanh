---
title : "Configure Cognito Email using SES"
date : 2024-01-01 
weight : 4
chapter : false
pre : " <b> 5.4.6. </b> "
---

#### Concept:
By default, Amazon Cognito dispatches system emails to users utilizing its own internal email server. However, this default provider is subject to lower daily limits and reduced delivery reliability.

For production configurations, Cognito supports direct integration with **Amazon SES** to send messages from a verified sender address (SES Identity). This integration improves email delivery rates and scales the daily sending capacity.

#### Configuration Steps:

1. Select your User Pool -> Click the **Messaging** tab.
- Find the **Email** section -> Click **Edit**.

![Edit Email Configuration](/images/5-Workshop/5.4-Cognito-SES/SES4.6.png)

2. Integrate SES as the email provider:
- In the **Email provider** section, select **Send email with Amazon SES (recommended)**.
- Under **SES Identity**, select the sender email address you previously verified in the [SES Configuration Step](../5.4.3-configure-ses).
- Configure the message parameters (e.g., Sender name, Reply-to email address if needed).
- Click **Save changes** to apply the configuration.

![Save Changes](/images/5-Workshop/5.4-Cognito-SES/SES4.7.png)
