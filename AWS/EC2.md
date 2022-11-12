# EC2 - Elastic Cloud Compute

- [Instance Types](#instance-types)
- [Hibernation](#hibernation)
- [Reserved Instances](#reserved-instances)
- [Auto Scaling](#auto-scaling)
    - [Scheduled Scaling Policy](#scheduled-scaling-policy)
    - [Launch Configuration](#launch-configuration)
    - [Termination Policies](#termination-policies)
        - [Default Termination Policy](#default-termination-policy)
- [**EBS**](#ebs)
    - [EBS Volume Types](#ebs-volume-types-ebsvt)
    - [Data Lifecycle Manager (DLM)](#amazon-data-lifecycle-manager-amazon-dlm)
- [**AMI**](#amazon-machine-images-ami)
    - [Recycle Bin](#recycle-bin)
- [Compute Optimizer](#aws-compute-optimizer-co)
- [Elastic Network Interface](#elastic-network-interfaces-eni)

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

## Hibernation

Hibernation of the Amazon EC2 instance can be used in the case of *memory-intensive applications or if applications take a long time to bootstrap*. Hibernation pre-warms the instance, and after resuming it, it quickly brings all application processes to a running state. When an instance is hibernated, the Amazon EC2 instance *saves all the content of the instance memory RAM to Amazon EBS volumes*. Any root EBS volumes or attached EBS volumes are persisted during hibernation.

Once an EC2 instance is started from the hibernation state, the following activities are performed:
- The EBS root volume and attached EBS volumes are reattached.
- The RAM contents are reloaded back to the instance memory from the EBS volumes.
- Application processes running before hibernation are back to the original state.
- The instance ID is not changed.

The above activities ensure that the applications running on the Amazon EC2 instance are quickly back to the production level after the hibernation state of the instance. 

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

### Scheduled scaling policy

Scaling based on a schedule allows you to scale your application in response to predictable load changes. For example you can scale up on busy days of the week or times of day. To configure your Auto Scaling group to scale based on a schedule, you create a **scheduled action**. The scheduled action tells Amazon EC2 Auto Scaling to perform a scaling action at specified times. To create a scheduled scaling action, *you specify the start time when the scaling action should take effect, and the new minimum, maximum, and desired sizes for the scaling action*. At the specified time, Amazon EC2 Auto Scaling updates the group with the values for minimum, maximum, and desired size specified by the scaling action. *You can create scheduled actions for scaling one time only or for scaling on a recurring schedule*.

### Launch configuration

You can only specify *one launch configuration* for an Auto Scaling group at a time, and you ***can’t modify a launch configuration after you’ve created it***. Therefore, if you want to change the launch configuration for an Auto Scaling group, you must create a launch configuration and then update your Auto Scaling group with the new launch configuration.

### Termination Policies

- [Default](#default-termination-policy)
- AllocationStrategy
- OldestLaunchTemplate
- OldestLaunchConfiguratoin
- ClosestToNextInstanceHour
- NewestInstance
- OldestInstance

#### Default Termination Policy

The default termination policy is designed to help ensure that your network architecture spans Availability Zones evenly. With the default termination policy, the behavior of the Auto Scaling group is as follows:
- If there are instances in multiple Availability Zones, choose the Availability Zone with the most instances and at least one instance that is not protected from scale in. If there is more than one Availability Zone with this number of instances, choose the Availability Zone with the instances that use the oldest launch configuration.
- Determine which unprotected instances in the selected Availability Zone use the oldest launch configuration. If there is one such instance, terminate it.
- If there are multiple instances to terminate based on the above criteria, determine which unprotected instances are closest to the next billing hour. (This helps you maximize the use of your EC2 instances and manage your Amazon EC2 usage costs.) If there is one such instance, terminate it.
- If there is more than one unprotected instance closest to the next billing hour, choose one of these instances at random.

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

### EBS Volume Types [^EBSVT]

- **General Purpose (SSD)** is the new, SSD-backed, general purpose EBS volume type that is recommended as the default choice for customers. General Purpose (SSD) volumes are suitable for a broad range of workloads, including small to medium-sized databases, development and test environments, and boot volumes.
- **Provisioned IOPS (SSD)** volumes offer storage with consistent and low-latency performance and are designed for I/O intensive applications such as large relational or NoSQL databases. Magnetic volumes provide the lowest cost per gigabyte of all EBS volume types.
- **Magnetic** volumes are ideal for workloads where data are accessed infrequently, and applications where the lowest storage cost is important. Take note that this is a Previous Generation Volume. The latest low-cost magnetic storage types are Cold HDD (sc1) and Throughput Optimized HDD (st1) volumes.

### Amazon Data Lifecycle Manager (Amazon DLM)

You can use Amazon Data Lifecycle Manager (Amazon DLM) to automate the creation, retention, and deletion of snapshots taken to back up your Amazon EBS volumes. Automating snapshot management helps you to:
- Protect valuable data by enforcing a regular backup schedule.
- Retain backups as required by auditors or internal compliance.
- Reduce storage costs by deleting outdated backups.

Combined with the monitoring features of Amazon CloudWatch Events and AWS CloudTrail, Amazon DLM provides a complete backup solution for EBS volumes at no additional cost. [^DLM]

## Amazon Machine Images (AMI)

An Amazon Machine Image (AMI) is a supported and maintained image provided by AWS that provides the information required to launch an instance. You must specify an AMI when you launch an instance. You can launch multiple instances from a single AMI when you require multiple instances with the same configuration. You can use different AMIs to launch instances when you require instances with different configurations.

### Recycle Bin

Recycle Bin is a data recovery feature that enables you to restore accidentally deleted Amazon EBS snapshots and EBS-backed AMIs. When using Recycle Bin, if your resources are deleted, they are retained in the Recycle Bin for a time period that you specify before being permanently deleted. [^RB]

## AWS Compute Optimizer [^CO]

AWS Compute Optimizer recommends optimal AWS resources for your workloads to reduce costs and improve performance by using machine learning to analyze historical utilization metrics. ***AWS Compute Optimizer can give recommendations if specific instances are under-provisioned, optimal, or over-provisioned***. You must opt-in to have Compute Optimizer analyze your AWS resources. Compute Optimizer generates recommendations for the following resources:
- Amazon Elastic Compute Cloud (Amazon EC2) instances
- Amazon EC2 Auto Scaling groups
- Amazon Elastic Block Store (Amazon EBS) volumes
- AWS Lambda functions

## Elastic Network Interfaces (ENI)

- An elastic network interface is a logical networking component in a VPC that represents a virtual network card, which directs traffic to your instance
- Every instance in a VPC has a default network interface, called the primary network interface (eth0). 
- You cannot detach a primary network interface from an instance.
- You can create and attach additional network interfaces. The maximum number of network interfaces that you can use varies by instance type.
- You can attach a network interface to an instance in a different subnet as long as its within the same AZ

If one of your instances serving a particular function fails, its network interface can be attached to a replacement or hot standby instance pre-configured for the same role in order to rapidly recover the service. For example, you can use a network interface as your primary or secondary network interface to a critical service such as a database instance or a NAT instance. If the instance fails, you (or more likely, the code running on your behalf) can attach the network interface to a hot standby instance. 

Because the interface maintains its private IP addresses, Elastic IP addresses, and MAC address, network traffic begins flowing to the standby instance as soon as you attach the network interface to the replacement instance. Users experience a brief loss of connectivity between the time the instance fails and the time that the network interface is attached to the standby instance, but no changes to the route table or your DNS server are required.

## *Resources*

- [Tutorials Dojo Cheat Sheet](https://tutorialsdojo.com/amazon-elastic-compute-cloud-amazon-ec2/)
- [AWS Reserved Instances types docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/reserved-instances-types.html)
- [Auto Scaling Cheat Sheet](https://tutorialsdojo.com/aws-auto-scaling/)
- [EBS Cheat Sheet](https://tutorialsdojo.com/aws-cheat-sheet-amazon-ebs/)

[^EBSVT]: [AWS EBS Volume Types docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSVolumeTypes.html)
[^DLM]: [AWS DLM snapshot lifecycle docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/snapshot-lifecycle.html)
[^RB]: [AWS Recycle Bin docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/recycle-bin-working-with-amis.html)
[^CO]: [AWS Computer Optimizer docs](https://docs.aws.amazon.com/compute-optimizer/latest/ug/what-is-compute-optimizer.html)