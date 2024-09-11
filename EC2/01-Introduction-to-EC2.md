# Amazon EC2 Quick Notes

### 🚀 What is EC2?
- **Amazon EC2 (Elastic Compute Cloud)**: Virtual servers in the cloud to run our applications.

### 🌟 Key Features
- **Scalable**: Adjust server capacity as per needed.
- **Flexible**: Choose instance types based on our needs.
- **Pay-as-you-go**: Pay only for what we use.

### 🛠️ Basic Concepts
- **Instance**: A virtual server.
- **AMI**: Template with OS and software.
- **Instance Types**:
  - `t3.micro` - Small, general-purpose.
  - `c5.large` - For compute-heavy tasks.
  - `r5.large` - For memory-intensive tasks.

### 💰 Pricing Models
- **On Demand**: Pay by the hour/second. *- No commitment. Stay and leave whenever you want.*
- **Reserved**: Save money with a 1-3 year commitment. *- Plan to stay for long time and get discounts*
- **Spot**: Bid on unused capacity at lower prices. *- Spot instances: Stay for the night in cheap price, but can be thrown out when someone pays more than you.*
- **Dedicated Host**: Fully dedicated physical server for our use. *- Book Entire Building.*
- **Dedicated Instances**:Dedicated hardware to launch our instance only. *- Book one room.*

**[EC2 Pricing Models](https://aws.amazon.com/pricing/?aws-products-pricing.sort-by=item.additionalFields.productNameLowercase&aws-products-pricing.sort-order=asc&awsf.Free%20Tier%20Type=*all&awsf.tech-category=*all)**

### 📝 Getting Started
1. **Choose an AMI**: Select OS/software.
2. **Pick an Instance Type**: Size your server.
3. **Set Security Groups**: Control access.
4. **Launch**: Start and connect to your instance.

### 🔑 Important Concepts
- **Elastic IP**: Static IP address.
- **Security Groups**: Firewall rules for your instance.
- **EBS**: Persistent storage.

### 📌 Tips
- **Start Small**: Use a free tier `t3.micro` to learn.
- **Backup**: Take snapshots of your data.
- **Monitor**: Use CloudWatch for performance and cost tracking.

### 📚 Resources
- **[AWS Free Tier](https://aws.amazon.com/free/)**: 750 hours/month on `t2.micro`.
- **[AWS Documentation](https://docs.aws.amazon.com/ec2/)**: Learn more.