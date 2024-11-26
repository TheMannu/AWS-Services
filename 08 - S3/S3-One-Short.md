### What is an S3 Bucket?

An **S3 bucket** is a storage container in Amazon's Simple Storage Service (S3) that holds data in the form of objects. These objects consist of the actual data (e.g., files) and associated metadata. Instead of a hierarchical file system like traditional storage, S3 employs a flat structure, where each object is assigned a unique key (identifier) within a bucket.

**Example:**
If you're building a photo-sharing app, you can create an S3 bucket called `my-photo-app`. All user-uploaded images will be stored as objects in this bucket, each with a unique key like `images/user1/photo1.jpg`.

### S3 Availability

Amazon S3 is designed to provide **99.999999999% (11 nines)** of durability and **99.99% availability** over a given year. Data in S3 is automatically distributed across at least **three geographically separated availability zones** in a region. This ensures that even if one or more data centers go offline, your data remains safe and accessible.

**Example:**
If you're running an e-commerce platform where uptime is crucial, S3 ensures that your product images and assets are always available to your customers without worrying about hardware failures.
