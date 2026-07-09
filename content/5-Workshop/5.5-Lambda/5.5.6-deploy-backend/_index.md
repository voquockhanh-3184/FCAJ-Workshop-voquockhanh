---
title : "Deploy Backend Code to Lambda"
date : 2024-01-01 
weight : 6
chapter : false
pre : " <b> 5.5.6. </b> "
---

After integrating the wrapper library and adjusting the Express application structure, we will package and deploy the backend codebase to AWS Lambda as a `.zip` deployment archive.

#### Step-by-Step Instructions:

1. Package the Application:
   * From the root directory of your backend project, compress the following files and folders into a `.zip` archive (e.g., `backend.zip`):
     * The source directory: `src/` (or `dist/` if transpiling TypeScript).
     * Production dependencies: `node_modules/`.
     * Configuration files: `package.json` and `package-lock.json`.
   * *Note*: Compress the files directly rather than compressing the parent folder itself. This ensures that the application files and dependencies sit at the root of the `.zip` archive.

2. Upload the Deployment Package to Lambda:
   * Navigate to the [Functions](https://ap-southeast-1.console.aws.amazon.com/lambda/home?region=ap-southeast-1#/functions) page in the Lambda console -> select the `examora-backend-api` function -> click the **Code** tab.
   * In the **Code source** panel, click **Upload from** in the top right -> choose **.zip file**.
   * Click **Upload**, select the `backend.zip` file, and click **Save** to upload the package.

   ![Upload .zip Archive](/images/5-Workshop/5.5-Lambda/5.5.6-deploy-backend/LambdaNen5.1.png)

3. Configure the Runtime Handler:
   * By default, AWS Lambda searches for an `index.js` file exporting a `handler` function at the root level. Since our entrypoint is located in `src/lambda.js` and exports `handler` (`module.exports.handler = ...`), we must update the handler configuration path:
   * Scroll down to the **Runtime settings** section under the Code tab -> click **Edit**.
   * In the **Handler** text box, update the value to: **`src/lambda.handler`**.
   * Click **Save** to apply the configuration.

   ![Edit Runtime Handler](/images/5-Workshop/5.5-Lambda/5.5.6-deploy-backend/LambdaNen5.2.png)
