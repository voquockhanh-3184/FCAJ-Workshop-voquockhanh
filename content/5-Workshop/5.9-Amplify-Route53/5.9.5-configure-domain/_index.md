---
title : "Map Custom Domain to Amplify"
date : 2024-01-01 
weight : 5
chapter : false
pre : " <b> 5.9.5. </b> "
---

#### Step-by-Step Instructions:

1. Initiate Custom Domain Mapping in AWS Amplify:
   * Navigate to the **AWS Amplify** app console.
   * In the left sidebar -> under the **Hosting** section -> choose **Custom domains** -> click **Add domain**.

   ![Select Custom domains](/images/5-Workshop/5.9-Amplify-Route53/5.9.5-configure-domain/GanDomain1.png)

2. Select Domain and Configure Routing Rules:
   * Choose your custom domain name managed in Route 53 (e.g., `examora.click`).
   * Click **Configure domain**.

   ![Select domain managed by Route 53](/images/5-Workshop/5.9-Amplify-Route53/5.9.5-configure-domain/GanDomain2.png)

   * Define the subdomain mapping constraints:
     * Route the apex root domain (e.g., `examora.click`) to point to the production branch (e.g., `main`).
     * Route the `www` subdomain (e.g., `www.examora.click`) to point to the production branch (e.g., `main`).
   * Click **Save** (or **Add domain**). AWS Amplify automatically initiates SSL/TLS certificate provisioning through AWS Certificate Manager (ACM) and updates the required CNAME and alias records in the corresponding Route 53 Hosted Zone.

   ![Configure Subdomain Mapping](/images/5-Workshop/5.9-Amplify-Route53/5.9.5-configure-domain/GanDomain3.png)

   * Await certificate validation and DNS mapping checks. Once the **Status** column displays a green **Available** flag, the custom domain setup is complete.

   ![Custom Domain Status Available](/images/5-Workshop/5.9-Amplify-Route53/5.9.5-configure-domain/GanDomain4.png)

3. Add Custom Domains to API Gateway CORS Allowed Origins:
   * To allow client requests from the new custom domains to call the API Gateway endpoints, we must add them to the CORS config.
   * Navigate to **API Gateway** -> open `examora-api` -> select **CORS** -> choose **Configure**.
   * Add the custom domains to the **Access-Control-Allow-Origin** list:
     * `https://examora.click`
     * `https://www.examora.click`
   * Click **Save**.

   ![Add Custom Domains to CORS list](/images/5-Workshop/5.9-Amplify-Route53/5.9.5-configure-domain/GanDomain5.png)

4. Update Lambda Backend API Environment Variables:
   * Open the **Lambda** console -> choose `examora-backend-api` -> navigate to the **Configuration** tab -> select **Environment variables** -> click **Edit**.
   * Set the `FRONTEND_ORIGIN` variable value to match your secure custom domain (e.g., `https://www.examora.click` or `https://examora.click`).
   * Click **Save** to apply.

   ![Update Lambda Environment Variables](/images/5-Workshop/5.9-Amplify-Route53/5.9.5-configure-domain/GanDomain6.png)

5. End-to-End Production Verification:
   * Open a web browser and navigate to `https://www.examora.click` or `https://examora.click`.
   ![Verify website via Custom Domain](/images/5-Workshop/5.9-Amplify-Route53/5.9.5-configure-domain/GanDomain7.png)

This completes the production deployment of the **Examora** online testing application, leveraging AWS serverless architecture to ensure high availability, security, and cost efficiency.
