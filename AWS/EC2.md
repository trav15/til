# EC2 - Elastic Cloud Compute

## Auto Scaling

In Auto Scaling, the following statements are correct regarding the cooldown period:
- It ensures that the Auto Scaling group does not launch or terminate additional EC2 instances before the previous scaling activity takes effect.
- Its default value is 300 seconds.
- It is a configurable setting for your Auto Scaling group.

## EBS
An Amazon EBS volume is a durable, block-level storage device that you can attach to a single EC2 instance. You can use **EBS volumes as primary storage** for data that requires frequent updates, such as the system drive for an instance or storage for a database application. You can also use them for throughput-intensive applications that perform continuous disk scans. ***EBS volumes persist independently from the running life of an EC2 instance***.

Here is a list of important information about EBS Volumes:
- When you create an EBS volume in an Availability Zone, it is **automatically replicated within that zone** to prevent data loss due to a failure of any single hardware component.
- After you create a volume, **you can attach it to any EC2 instance in the same Availability Zone**
- Amazon **EBS Multi-Attach** enables you to attach a single Provisioned IOPS SSD (io1) volume to multiple Nitro-based instances that are in the same Availability Zone. However, other EBS types are not supported.
- An EBS volume is off-instance storage that can persist independently from the life of an instance. **You can specify not to terminate the EBS volume when you terminate the EC2 instance** during instance creation.
- **EBS volumes support live configuration changes while in production** which means that you can modify the volume type, volume size, and IOPS capacity without service interruptions.
- Amazon EBS encryption uses 256-bit Advanced Encryption Standard algorithms (AES-256)
- EBS Volumes offer 99.999% SLA.

### Amazon Data Lifecycle Manager (Amazon DLM)

You can use Amazon Data Lifecycle Manager (Amazon DLM) to automate the creation, retention, and deletion of snapshots taken to back up your Amazon EBS volumes. Automating snapshot management helps you to:
- Protect valuable data by enforcing a regular backup schedule.
- Retain backups as required by auditors or internal compliance.
- Reduce storage costs by deleting outdated backups.

Combined with the monitoring features of Amazon CloudWatch Events and AWS CloudTrail, Amazon DLM provides a complete backup solution for EBS volumes at no additional cost.
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/snapshot-lifecycle.html

## AWS Compute Optimizer 

AWS Compute Optimizer recommends optimal AWS resources for your workloads to reduce costs and improve performance by using machine learning to analyze historical utilization metrics. ***AWS Compute Optimizer can give recommendations if specific instances are under-provisioned, optimal, or over-provisioned***. You must opt-in to have Compute Optimizer analyze your AWS resources. Compute Optimizer generates recommendations for the following resources:
- Amazon Elastic Compute Cloud (Amazon EC2) instances
- Amazon EC2 Auto Scaling groups
- Amazon Elastic Block Store (Amazon EBS) volumes
- AWS Lambda functions
