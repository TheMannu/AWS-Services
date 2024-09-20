Breakdown of **Vertical Scaling** and **Horizontal Scaling** in cloud environments like AWS

### Vertical Scaling (Scaling Up)
- **Definition**: Increasing the resources (such as CPU, memory, storage) of a single instance/server.
- **Example**: 
  - Running an application on a t2.micro instance with 2 CPUs and 2GB RAM.
  - Scaling vertically means Upgrading an EC2 instance from a t2.micro (2 CPU, 2 GB RAM) to a t2.large (4 CPU, 4 GB RAM).
- **Common Use Cases**:
  - This is often used for non-distributed systems, such as databases like Amazon RDS or ElastiCache, where increasing the instance size is more practical than adding more instances.
- **Limitations**:
  - There is typically a hardware limit to how much an instance can scale vertically. Once the instance reaches its maximum size, further scaling is not possible.