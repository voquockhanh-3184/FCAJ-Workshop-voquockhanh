---
title : "Create Lambda Function"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.5.3. </b> "
---

In this step, we will create the core Lambda function that will host and execute the Express backend of the Examora system.

#### Step-by-Step Instructions:

1. Create Lambda Function:
   * In the AWS Console search bar, search for **Lambda** -> select **Functions** in the left navigation pane -> click **Create function**.
   * Choose **Author from scratch**.
   * Configure the basic function details:
     * **Function name**: Enter `examora-backend-api`.
     * **Runtime**: Select **Node.js 22.x**
     * **Architecture**: Select **x86_64**.
     * **Permissions**: Expand **Change default execution role** -> choose **Use an existing role** -> search for and select the IAM execution role created in the previous step (e.g., `examora-lambda-backend-role`).
   * Click **Create function** and wait for the initialization to complete.

   ![Configure Function Parameters](/images/5-Workshop/5.5-Lambda/5.5.3-create-lambda-function/LamdaFuctions5.1.png)

   ![Select Execution Role](/images/5-Workshop/5.5-Lambda/5.5.3-create-lambda-function/LamdaFuctions5.2.png)

2. Configure Lambda Runtime Settings:
   * Select the newly created function -> navigate to the **Configuration** tab -> choose **General configuration** -> click **Edit**, configure settings as appropriate for the Express backend -> click **Save**.

   ![Adjust General Configuration](/images/5-Workshop/5.5-Lambda/5.5.3-create-lambda-function/LamdaFuctions5.3.png)
