# Security

A **defense-in-depth strategy** is one of the design principles for security in the AWS cloud. This strategy entails *implementing security controls at multiple layers* (for example, edge of network, VPC, load balancing, every instance and compute service, operating system, application, and code).

Components such as EC2 instances, RDS database clusters, and Lambda functions that share reachability requirements **can be segmented into layers formed by subnets**. For example, an RDS database cluster in a VPC with no need for internet access should be placed in subnets with no route to or from the internet. *This layered approach for the controls mitigates the impact of a single layer misconfiguration, which could allow unintended access*.

## Security Groups

A **security group**[^sg] acts as a virtual firewall that controls the traffic for one or more instances. When you launch an instance, you associate one or more security groups with the instance. You add rules to each security group that control traffic based on protocols and port numbers. There are separate sets of rules for inbound traffic and outbound traffic. You can modify the rules for a security group at any time; the new rules are automatically applied to all instances that are associated with the security group.

A security group determines what traffic is permitted in/out of a resource on a virtual network. Therefore, think about what can be launched "into" a virtual network:

- Amazon EC2 instances
- Services that launch EC2 instances:
    - AWS Elastic Beanstalk
    - Amazon Elastic MapReduce
- Services that use EC2 instances (without appearing directly in the EC2 service):
    - Amazon RDS (Relational Database Service)
    - Amazon Redshift
    - Amazon ElastiCache
    - Amazon CloudSearch
- Elastic Load Balancing
- Lambda

**Resources do not "belong" to a security group**. Rather, one or more Security Groups are associated to a resource. This is often a difficult concept to understand since Security Groups have similar abilities to firewalls, and firewalls generally "encase" a number of devices. Rather than "belonging to", or "being encased by", a security group, the virtual network simply uses the definitions contained within a security group to determine what traffic to permit in/out of the resource.

[^sg]: [AWS Security Groups docs](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#working-with-security-groups)