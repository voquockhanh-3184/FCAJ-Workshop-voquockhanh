---
title : "Create IAM User and Enable MFA"
date : 2024-01-01 
weight : 4
chapter : false
pre : " <b> 5.2.4. </b> "
---

1. In the **IAM Dashboard** (left menu), select **Users** -> Click **Create user** to start creating an IAM User:

![Create User](/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.1.png)

2. Configure the necessary user details:

- **Step 1**: Specify the username for the IAM User:

![Set User Name](/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.2.png)

- **Step 2**: Add the user to the `ExamoraAdminGroup` created earlier to assign administrative permissions:

![Add User to Group](/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.3.png)

- **Step 3**: Review the user details and click **Create user** to complete the creation:

![Review and Create](/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.4.png)

- Similarly, create other IAM users for other team members but with appropriate, lower privileges.
- Least privilege access helps manage permissions clearly and reduces the risk of sharing the Root account or sharing a single IAM user.

![IAM Users List](/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.5.png)

3. Enable MFA (Multi-Factor Authentication) for the IAM user to enhance AWS Console sign-in security:

{{% notice note %}}
Regarding access keys, only create them for users who need to use the AWS CLI or SAM to deploy/cleanup resources. Do not create access keys for all members.
{{% /notice %}}

- Click on the user that needs MFA, then select the **Security credentials** tab.
- Under **Multi-factor authentication (MFA)**, choose **Assign MFA device**:

![Assign MFA Device](/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.6.png)

- Name the MFA device and select the authentication method:

![Set MFA Device](/images/5-Workshop/5.2-IAM/5.2.4-create-iam-user/IAM3.7.png)
