# VPC (Virtual Private Cloud)

Amazon Virtual Private Cloud (VPC) is a service that lets you launch AWS resources in a logically isolated virtual network that you define. You have complete control over your virtual networking environment, including selection of your own IP address range, creation of subnets, and configuration of route tables and network gateways. You can use both IPv4 and IPv6 for most resources in your virtual private cloud, helping to ensure secure and easy access to resources and applications.

A **subnet** is a range of IP addresses in your VPC. You can launch AWS resources into a specified subnet. When you create a VPC, you must specify a range of IPv4 addresses for the VPC in the form of a CIDR block. ***Each subnet must reside entirely within one Availability Zone and cannot span zones***. You can also *optionally assign an IPv6 CIDR block to your VPC*, and assign IPv6 CIDR blocks to your subnets. Again, *IPv4 CIDRs are required*.

If you have an existing VPC that supports IPv4 only and resources in your subnet that are configured to use IPv4 only, you can enable IPv6 support for your VPC and resources. Your VPC can operate in dual-stack mode — your resources can communicate over IPv4, or IPv6, or both. IPv4 and IPv6 communication are independent of each other. ***You cannot disable IPv4 support for your VPC and subnets since this is the default IP addressing system for Amazon VPC and Amazon EC2***.

## Intra/Inter communication

***By default, instances that you launch into a virtual private cloud (VPC) can’t communicate with your own network***. You can enable access to your network from your VPC by attaching a virtual private gateway to the VPC, creating a custom route table, updating your security group rules, and creating an AWS managed VPN connection.

Although the term VPN connection is a general term, *in the Amazon VPC documentation, a VPN connection refers to the connection between your VPC and your own network*. AWS supports Internet Protocol security (IPsec) VPN connections. A **customer gateway** is a physical device or software application on your side of the VPN connection. To create a VPN connection, ***you must create a customer gateway resource in AWS, which provides information to AWS about your customer gateway device***. Next, you have to set up an Internet-routable IP address (static) of the customer gateway’s external interface.

To check that two EC2 instances can communicate inside a VPC, first, the Network ACL should be properly set to allow communication between the two subnets. Second, the security group should also be properly configured so that your web server can communicate with the database server.

## VPC Endpoint

A VPC endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by AWS PrivateLink without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection. ***Instances in your VPC do not require public IP addresses to communicate with resources in the service***. Traffic between your VPC and the other service does not leave the Amazon network.

When you create a VPC endpoint, ***you can attach an endpoint policy that controls access to the service to which you are connecting***. You can modify the endpoint policy attached to your endpoint and add or remove the route tables used by the endpoint. An endpoint policy does not override or replace IAM user policies or service-specific policies (such as S3 bucket policies). It is a separate policy for controlling access from the endpoint to the specified service. https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints-s3.html

## Network Firewall

AWS Network Firewall is a *stateful, managed network firewall and intrusion detection and prevention service for your virtual private cloud (VPC)* that you create in Amazon Virtual Private Cloud (Amazon VPC). With Network Firewall, you can filter traffic at the perimeter of your VPC. This includes filtering traffic going to and coming from an internet gateway, NAT gateway, or over VPN or AWS Direct Connect. Network Firewall uses the open source intrusion prevention system (IPS), Suricata, for stateful inspection. Network Firewall supports Suricata compatible rules. *AWS Network Firewall supports domain name stateful network traffic inspection*. You can create Allow lists and Deny lists with domain names that the stateful rules engine looks for in network traffic.

## *Resources*

- [Tutorials Dojo VPC Cheat Sheet](https://tutorialsdojo.com/amazon-vpc/)
- [AWS VPC Endpoints docs](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints-s3.html)