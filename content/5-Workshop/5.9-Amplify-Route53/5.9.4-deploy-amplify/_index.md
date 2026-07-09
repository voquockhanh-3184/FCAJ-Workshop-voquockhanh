---
title : "Deploy to AWS Amplify Hosting"
date : 2024-01-01 
weight : 4
chapter : false
pre : " <b> 5.9.4. </b> "
---

#### Step-by-Step Instructions:

1. Deploy Frontend Bundle to AWS Amplify:
   * Search for **AWS Amplify** in the AWS management console search bar.
   * Click **Create new app**.
   * Under the *Start building with Amplify* section -> select **Deploy without Git** -> click **Next**.

   ![Select Deploy without Git](/images/5-Workshop/5.9-Amplify-Route53/5.9.4-deploy-amplify/Amplify1.png)

   * Configure application deployment attributes:
     * **App name**: Enter a name (e.g., `examora-frontend`).
     * **Branch name**: Enter `main`.
     * **Method**: Drag and drop the `.zip` archive prepared in step 5.9.3.
   * Click **Save and deploy** to trigger the manual deployment workflow.

   ![Upload ZIP and Deploy](/images/5-Workshop/5.9-Amplify-Route53/5.9.4-deploy-amplify/Amplify2.png)

   * Upon completion, AWS Amplify provisions a default domain with the following format: `https://main.xxxxxx.amplifyapp.com`.

   ![Deployment Succeeded](/images/5-Workshop/5.9-Amplify-Route53/5.9.4-deploy-amplify/Amplify3.png)

   * Click the generated URL link. If the Examora login screen renders correctly, the baseline deployment is successful.

   ![Access Login Page via Amplify Domain](/images/5-Workshop/5.9-Amplify-Route53/5.9.4-deploy-amplify/Amplify4.png)

2. Configure Single Page Application (SPA) Rewrites and Redirects:
   * Because React applications utilize client-side routing, navigation refreshes on sub-routes (e.g., `/dang-nhap`, `/lich-su-thi`) will return HTTP 404 errors. We must configure a rewrite rule to direct all path traffic to `index.html`.
   * From the Amplify application dashboard sidebar -> navigate to **Hosting** -> choose **Rewrites and redirects** -> click **Manage redirects**.

   ![Hosting Redirect Settings](/images/5-Workshop/5.9-Amplify-Route53/5.9.4-deploy-amplify/Amplify5.png)

   * Click **Add rule** or modify the default rules to match:
   * Click **Save** to apply the rule. This prevents 404 response errors when users refresh application sub-routes.

   ![Configure Redirect Rules](/images/5-Workshop/5.9-Amplify-Route53/5.9.4-deploy-amplify/Amplify6.png)

   ![Save Redirect Rules](/images/5-Workshop/5.9-Amplify-Route53/5.9.4-deploy-amplify/Amplify7.png)

3. Update API Gateway CORS Configurations:
   * Since the frontend is hosted on the new AWS Amplify origin, we must add this URL to the API Gateway CORS allowance settings to prevent cross-origin resource sharing blocks.
   * Go to **API Gateway** -> select `examora-api` -> click **CORS** -> choose **Configure**.
   * Under **Access-Control-Allow-Origin** -> add the default Amplify application domain URL -> click **Save**.

   ![CORS Settings in API Gateway](/images/5-Workshop/5.9-Amplify-Route53/5.9.4-deploy-amplify/CORS5.9.png)

4. Update Lambda Backend API Environment Variables:
   * Go to the **Lambda** console -> choose `examora-backend-api` -> open **Configuration** -> choose **Environment variables** -> click **Edit**.
   * Update the `FRONTEND_ORIGIN` variable value to match the default Amplify application URL.
   * Click **Save**.

   ![Update Lambda Environment Variables](/images/5-Workshop/5.9-Amplify-Route53/5.9.4-deploy-amplify/LambdaBE5.9.png)

5. Package, Redeploy, and Verify:
   * Compress the local Frontend code bundle configured with the API Gateway endpoints, then upload the `.zip` archive again to Amplify.
   * Navigate to the default Amplify application URL, log in as a student, and verify that all REST endpoints resolve correctly.

   ![E2E Application Testing](/images/5-Workshop/5.9-Amplify-Route53/5.9.4-deploy-amplify/TestAmplify1.png)
