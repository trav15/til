# EC2 - Elastic Cloud Compute

## Instance Types
| Instance Family | Type | Use |
| --- | --- | --- |
| General Purpose | T – cheap general purpose | Burstable performance instances|
| | M – Main choice general purpose apps | Fixed performance |
| Compute Optimized | C – Compute | Cost-effective high performance at a low price per compute ratio |
| Memory Optimized | R – RAM | Memory-intensive applications |
| | X – eXtreme memoryZ | Large-scale, enterprise-class, in-memory applications, and high-performance DBs |
| | Z-factor | Extreme memory and CPU |
| Accelerated Computing | P – Picture (graphics)| General purpose GPU instances |
| | G – Graphics | Graphics-intensive GPU instances |
| | F – FPGA | Reconfigurable FPGA instances |
| Storage Optimized | I – IOPSD – Density | High storage instances, low latency, high random I/O performance, high sequential read throughput, and high IOPS |
| | H – High disk throughput | HDD-based local storage for high disk throughput |

## Reserved Instances

Reserved Instances (RIs) provide you with a **significant discount (up to 75%)** compared to On-Demand instance pricing. You have the flexibility to change families, OS types, and tenancies while benefiting from RI pricing when you use Convertible RIs. One important thing to remember here is that ***Reserved Instances are not physical instances, but rather a billing discount applied to the use of On-Demand Instances*** in your account.

The offering class of a Reserved Instance is either **Standard** or **Convertible**. A Standard Reserved Instance provides a more significant discount than a Convertible Reserved Instance, but *you can’t exchange a Standard Reserved Instance* unlike Convertible Reserved Instances. You can modify Standard and Convertible Reserved Instances. Take note that in Convertible Reserved Instances, ***you are allowed to exchange another Convertible Reserved instance with a different instance type and tenancy***.

The configuration of a Reserved Instance comprises a single instance type, platform, scope, and tenancy over a term. When your computing needs change, you can modify your Standard or Convertible Reserved Instances and continue to take advantage of the billing benefit. You can modify the Availability Zone, scope, network platform, or instance size (within the same instance type) of your Reserved Instance. ***You can also sell your unused instance for Standard RIs but not Convertible RIs on the Reserved Instance Marketplace***.

## Auto Scaling

An Auto Scaling group contains a collection of Amazon EC2 instances that are treated as a logical grouping for the purposes of automatic scaling and management. An Auto Scaling group also enables you to use Amazon EC2 Auto Scaling features such as *health check replacements and scaling policies*. Both maintaining the number of instances in an Auto Scaling group and automatic scaling are the core functionality of the Amazon EC2 Auto Scaling service. The size of an Auto Scaling group depends on the number of instances that you set as the desired capacity. You can adjust its size to meet demand, either manually or by using automatic scaling.

With a target tracking scaling policy, you can increase or decrease the current capacity of the group based on a target value for a specific metric. This policy will help resolve the over-provisioning of your resources. The scaling policy adds or removes capacity as required to keep the metric at, or close to, the specified target value. In addition to keeping the metric close to the target value, a target tracking scaling policy also adjusts to changes in the metric due to a changing load pattern.

In Auto Scaling, the following statements are correct regarding the cooldown period:
- It ensures that the Auto Scaling group does not launch or terminate additional EC2 instances before the previous scaling activity takes effect.
- Its default value is 300 seconds.
- It is a configurable setting for your Auto Scaling group.

**Scheduled scaling policy** - Scaling based on a schedule allows you to scale your application in response to predictable load changes. For example you can scale up on busy days of the week or times of day. To configure your Auto Scaling group to scale based on a schedule, you create a **scheduled action**. The scheduled action tells Amazon EC2 Auto Scaling to perform a scaling action at specified times. To create a scheduled scaling action, *you specify the start time when the scaling action should take effect, and the new minimum, maximum, and desired sizes for the scaling action*. At the specified time, Amazon EC2 Auto Scaling updates the group with the values for minimum, maximum, and desired size specified by the scaling action. *You can create scheduled actions for scaling one time only or for scaling on a recurring schedule*.

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

## *Resources*

- [Tutorials Dojo Cheat Sheet](https://tutorialsdojo.com/amazon-elastic-compute-cloud-amazon-ec2/)
- [AWS Reserved Instances types docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/reserved-instances-types.html)
- [Auto Scaling Cheat Sheet](https://tutorialsdojo.com/aws-auto-scaling/)
- [EBS Cheat Sheet](https://tutorialsdojo.com/aws-cheat-sheet-amazon-ebs/)
- [AWS DLM docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/snapshot-lifecycle.html)
- [AWS Computer Optimizer docs](https://docs.aws.amazon.com/compute-optimizer/latest/ug/what-is-compute-optimizer.html)