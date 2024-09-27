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

### Step 3: Upload Website Files to the S3 Bucket
1. In your bucket, navigate to the **Objects** tab.
2. Click **Upload** and select the website files (e.g., `index.html`, `error.html`, `CSS`/`JS` files).
3. Click **Add files** or **Add folder** to upload all your website resources.
4. Click **Upload**.

### Step 4: Configure Bucket Permissions for Public Access
1. Go to the **Permissions** tab in your bucket.
2. Scroll down to **Bucket Policy** and click **Edit**.
3. Add the following **bucket policy** to make your bucket publicly accessible:
   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Sid": "PublicReadGetObject",
         "Effect": "Allow",
         "Principal": "*",
         "Action": "s3:GetObject",
         "Resource": "arn:aws:s3:::my-static-website/*"
       }
     ]
   }
   ```
   Replace `my-static-website` with your bucket's name.
4. Click **Save changes**.

### Step 5: Access Your Static Website
1. Go back to the **Properties** tab of your bucket.
2. Scroll down to **Static website hosting**.
3. You will see the **Bucket website endpoint** URL (e.g., `http://my-static-website.s3-website-us-east-1.amazonaws.com`).
4. Click the link or copy it to your browser to access your hosted static website.