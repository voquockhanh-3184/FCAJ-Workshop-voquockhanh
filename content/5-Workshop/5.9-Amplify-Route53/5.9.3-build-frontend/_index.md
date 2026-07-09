---
title : "Build and Package Frontend"
date : 2024-01-01 
weight : 3
chapter : false
pre : " <b> 5.9.3. </b> "
---

#### Step-by-Step Instructions:

1. Compile Frontend Codebase (React/Vite):
   * Open your command line interface in the root directory of the Frontend codebase.
   * Execute the build script to compile the application for production optimization:
     ```bash
     npm run build
     ```
   * Upon compilation, a `dist/` output directory is generated containing all optimized static bundle assets (HTML, CSS, JavaScript, images, etc.).

   ![Build Frontend Production Assets](/images/5-Workshop/5.9-Amplify-Route53/5.9.3-build-frontend/BuildFE.png)

2. Package Static Bundle Files:
   * Compress the entire content of the `dist/` directory.
   * **Critical Note:** You must open and enter the `dist/` directory, select all of its files and folders, and compress them into a `.zip` file (e.g., `dist.zip`). Do not compress the root `dist/` directory itself from the outside, as nesting files under a parent folder will cause routing and file loading failures when deployed on AWS Amplify.

   ![Compress dist Folder Contents](/images/5-Workshop/5.9-Amplify-Route53/5.9.3-build-frontend/BuildFE2.png)
