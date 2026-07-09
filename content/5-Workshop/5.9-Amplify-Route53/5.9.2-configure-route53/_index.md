---
title : "Configure Amazon Route 53 for Custom Domain"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.9.2. </b> "
---

#### Step-by-Step Instructions:

1. Initialize Hosted Zone on Amazon Route 53:
   * Navigate to the **Amazon Route 53** console -> choose **Hosted zones** in the left navigation pane -> click **Create hosted zone**.
   * If you do not own a domain name, click *Register a domain* to purchase one directly via AWS.
   * If you own a domain from an external registrar (e.g., Namecheap, GoDaddy, Mắt Bão, etc.):
     * **Domain name**: Enter your registered domain name (e.g., `examora.click`).
     * **Type**: Select `Public hosted zone`.
     * Click **Create hosted zone** to provision the DNS zone.

   ![Access Route 53 Hosted Zones](/images/5-Workshop/5.9-Amplify-Route53/5.9.2-configure-route53/Route1.png)

   ![Hosted Zone Created](/images/5-Workshop/5.9-Amplify-Route53/5.9.2-configure-route53/Route2.png)

2. Retrieve AWS Name Servers:
   * Click on your newly created domain in the Hosted zones overview page.
   * In the **Records** tab, locate the record of type `NS` (Name Server) -> record the **4 AWS Name Server values** displayed.

   ![AWS Name Servers](/images/5-Workshop/5.9-Amplify-Route53/5.9.2-configure-route53/Route3.png)

3. Update Name Server Settings at Your Domain Registrar:
   * Sign in to your domain registrar dashboard.
   * Go to the **DNS Settings** or **Custom DNS Nameservers** section.
   * Replace the registrar default nameservers with the **4 AWS Name Server values** copied from Route 53 -> save settings.

4. Verify Domain Configuration:
   * Open your local terminal and run the lookup command:
     ```bash
     nslookup -type=NS <your_domain>
     ```
     *(Example: `nslookup -type=NS examora.click`)*.
   * If the output lists the AWS name server hostnames containing `awsdns`, DNS delegation has successfully propagated.

   ![Verify DNS with nslookup](/images/5-Workshop/5.9-Amplify-Route53/5.9.2-configure-route53/Route4.png)
