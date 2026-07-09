---
title : "Create IAM Admin Group"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.2.3. </b> "
---

1. In the **IAM Dashboard** (left menu), find and select **User groups**, then click **Create group**:

![Create Group](/images/5-Workshop/5.2-IAM/5.2.3-create-admin-group/IAM2.1.png)

2. Name the IAM group (e.g., `ExamoraAdminGroup`):

![Set Group Name](/images/5-Workshop/5.2-IAM/5.2.3-create-admin-group/IAM2.2.png)

3. Attach administrative policy: Scroll down to the **Attach permissions policies - Optional** section, search and select **AdministratorAccess** -> Click **Create user group** to create the group.

![Attach AdministratorAccess](/images/5-Workshop/5.2-IAM/5.2.3-create-admin-group/IAM2.3.png)

{{% notice info %}}
**AdministratorAccess** is temporarily used for the initial configuration phase.
{{% /notice %}}

4. User group created successfully:

![Group Created Successfully](/images/5-Workshop/5.2-IAM/5.2.3-create-admin-group/IAM2.4.png)
