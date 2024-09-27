Host a static website on Amazon S3 using the AWS Console.

### Step 1: Create an S3 Bucket
1. Log in to the **AWS Management Console**.
2. Navigate to **S3** by searching for "S3" in the services search bar.
3. Click on **Create bucket**.
4. Enter a **unique bucket name** (e.g., `my-static-website`).
5. Choose a region (preferably close to your audience).
6. **Uncheck** the option **"Block all public access"** under the "Bucket settings for Block Public Access" section. This is required to allow the public to view your website content.
7. Acknowledge that you are allowing public access by checking the confirmation box.
8. Click **Create bucket**.

### Step 2: Enable Static Website Hosting
1. Select the newly created bucket from your S3 dashboard.
2. Go to the **Properties** tab.
3. Scroll down to **Static website hosting** and click **Edit**.
4. Choose **Enable**.
5. Under **Hosting type**, select **Host a static website**.
6. Specify your website’s **index document** (e.g., `index.html`).
7. Optionally, specify an **error document** (e.g., `error.html`) for error handling.
8. Click **Save**.
