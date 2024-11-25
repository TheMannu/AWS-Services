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
3. You will see the **Bucket website endpoint** URL (e.g., (http://ashwani-kumar.s3-website-us-east-1.amazonaws.com)).
4. Click the link or copy it to your browser to access your hosted static website.

### Optional Step: Point a Custom Domain to Your S3 Website
If you want to use a custom domain (e.g., `www.mywebsite.com`), follow these additional steps:

1. **Register a Domain Name**: If you don't already have one, register a domain using Route 53 or another domain registrar.
2. **Create a Hosted Zone in Route 53**: 
   - Go to **Route 53** in the AWS Console.
   - Create a new **Hosted Zone** for your domain (e.g., `mywebsite.com`).
3. **Add an Alias Record**:
   - In the Hosted Zone, click **Create Record**.
   - Choose **Simple Routing**.
   - Select **A Record** and check the option to use an **Alias**.
   - In the **Alias Target**, select the **S3 website endpoint** for your bucket.
   - Click **Create records**.

Now, your custom domain will point to your S3 bucket, and your website will be accessible via your domain (e.g., `www.mywebsite.com`).

### Step 6: Set Up HTTPS with CloudFront (Optional)
To secure your website with HTTPS, use **CloudFront** as a CDN:
1. Go to the **CloudFront** service in AWS.
2. Click **Create Distribution**.
3. For the origin domain, use the **S3 bucket endpoint**.
4. Enable **Viewer Protocol Policy** to **Redirect HTTP to HTTPS**.
5. Set up a free **SSL/TLS certificate** using **AWS Certificate Manager (ACM)**.
6. Deploy the CloudFront distribution and use the provided CloudFront URL or map it to your custom domain.

---
---
### Portfolio - [Ashwani Kumar](http://ashwani-kumar.s3-website-us-east-1.amazonaws.com)
---
---

Hosting a static website on Amazon S3 using the AWS CLI:

### Prerequisites:
- **AWS CLI installed and configured** with appropriate IAM permissions to access and manage S3.
- A **domain name** if you wish to use Route 53 for DNS.
  
---
### Step 1: Create an S3 Bucket
The first step is to create an S3 bucket where your website files will be stored. The bucket name must be globally unique, and if you plan to use a custom domain, the bucket name should match the domain name.

```bash
aws s3 mb s3://your-domain-name.com
```

### Step 2: Enable Static Website Hosting
Next, configure the S3 bucket for static website hosting. This tells AWS S3 to treat the bucket as a web host for static content (e.g., HTML, CSS, JS).

```bash
aws s3 website s3://your-domain-name.com/ --index-document index.html --error-document error.html
```

- `--index-document`: The file that will be served when users access your website (usually `index.html`).
- `--error-document`: The file that will be served in case of an error (optional, e.g., `error.html`).


### Step 3: Set Bucket Policy for Public Access
By default, S3 buckets are private. To host a website, you'll need to make your bucket and its content publicly accessible. Create a bucket policy using a JSON file to allow public access to your static website.

**Create a file `bucket-policy.json`**:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-domain-name.com/*"
    }
  ]
}
```

**Apply the bucket policy**:

```bash
aws s3api put-bucket-policy --bucket your-domain-name.com --policy file://bucket-policy.json
```

### Step 4: Upload Website Files to S3
You can now upload your static website files (HTML, CSS, JS) to the S3 bucket.

```bash
aws s3 sync ./website-folder s3://your-domain-name.com/
```

This command syncs all files in your `website-folder` to the S3 bucket. Ensure that `index.html` is present in the root of this folder.

### Step 5: (Optional) Configure Custom Domain with Route 53

If you own a custom domain and want to use Route 53 to point it to your S3 bucket:

#### Step 5.1: Create a Hosted Zone in Route 53
In the Route 53 console or via CLI, create a hosted zone for your domain:

```bash
aws route53 create-hosted-zone --name your-domain-name.com --caller-reference <unique-string>
```

#### Step 5.2: Create an Alias Record to Point to S3
Create an **Alias Record** in Route 53 to point your domain to the S3 bucket.

**Example JSON file for the record set (`route53-record.json`)**:

```json
{
  "Comment": "Alias record for S3 static website",
  "Changes": [
    {
      "Action": "CREATE",
      "ResourceRecordSet": {
        "Name": "your-domain-name.com",
        "Type": "A",
        "AliasTarget": {
          "HostedZoneId": "Z3AQBSTGFYJSTF",  # S3 website hosted zone ID (for us-east-1)
          "DNSName": "your-domain-name.com.s3-website-us-east-1.amazonaws.com",
          "EvaluateTargetHealth": false
        }
      }
    }
  ]
}
```

Apply the Route 53 record change:

```bash
aws route53 change-resource-record-sets --hosted-zone-id <your-hosted-zone-id> --change-batch file://route53-record.json
```

### Step 6: Test the Website
Your static website should now be hosted on S3. If using Route 53, it may take a few minutes for DNS propagation, after which your website will be accessible via your custom domain.

You can also access the site directly via the S3 website URL:
```
http://your-domain-name.com.s3-website-<region>.amazonaws.com
```

---

### Additional (Optional) Steps:
1. **Enable SSL**: You can enable SSL/TLS with Amazon CloudFront to serve your website over HTTPS.
2. **Use CloudFront for CDN**: If you want to improve the performance of your static site globally, you can create a CloudFront distribution to cache your website content at edge locations.

A static website hosted on Amazon S3.