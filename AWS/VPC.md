# VPC (Virtual Private Cloud)

- [Subnets](#subnets)
- [Intra/Inter communication](#intrainter-communication)
- [VPC Endpoint](#vpc-endpoint)
    - [AWS PrivateLink](#aws-privatelink)
- [NAT Gateway](#nat-gateway-nat)
- [Invalid peering configurations](#invalid-peering-configurations)
- [Network Firewall](#network-firewall)
- [Bastion Host](#bastion-host)

Amazon Virtual Private Cloud (VPC) is a service that lets you launch AWS resources in a logically isolated virtual network that you define. You have complete control over your virtual networking environment, including selection of your own IP address range, creation of subnets, and configuration of route tables and network gateways. You can use both IPv4 and IPv6 for most resources in your virtual private cloud, helping to ensure secure and easy access to resources and applications. *A VPC can span multiple AZs*.

When you create a VPC, it comes with a default [security group](Security.md#security-groups). You can create additional security groups for each VPC. You can associate a security group only with resources in the VPC for which it is created.

## Subnets

A **subnet** is a range of IP addresses in your VPC. You can launch AWS resources into a specified subnet. When you create a VPC, you must specify a range of IPv4 addresses for the VPC in the form of a CIDR block. ***Each subnet must reside entirely within one Availability Zone and cannot span zones***. You can also *optionally assign an IPv6 CIDR block to your VPC*, and assign IPv6 CIDR blocks to your subnets. Again, **IPv4 CIDRs are required**.

Important things to remember about a subnets:
- Each subnet maps to a single Availability Zone.
- Every subnet that you create is automatically associated with the main route table for the VPC.
- If a subnet’s traffic is routed to an Internet gateway, the subnet is known as a public subnet.

### Subnet types

Depending on how you configure your VPC, subnets are considered public, private, or VPN-only:
- Public subnet: The subnet traffic is routed to the public internet through an internet gateway or an egress-only internet gateway. 
- Private subnet: The subnet traffic can't reach the public internet through an internet gateway or egress-only internet gateway. ***Access to the public internet requires a NAT device***.
- VPN-only subnet: The subnet traffic is routed to a Site-to-Site VPN connection through a virtual private gateway. The subnet traffic can't reach the public internet through an internet gateway. 

When you create a subnet, you specify its IP addresses, depending on the configuration of the VPC:
- IPv4 only: The subnet has an IPv4 CIDR block but does not have an IPv6 CIDR block. Resources in an IPv4-only subnet must communicate over IPv4.
- Dual stack: The subnet has both an IPv4 CIDR block and an IPv6 CIDR block. The VPC must have both an IPv4 CIDR block and an IPv6 CIDR block. Resources in a dual-stack subnet can communicate over IPv4 and IPv6.
- IPv6 only: The subnet has an IPv6 CIDR block but does not have an IPv4 CIDR block. The VPC must have an IPv6 CIDR block. Resources in an IPv6-only subnet must communicate over IPv6.

Regardless of the type of subnet, the internal IPv4 address range of the subnet is always private—AWS does not announce the address block to the internet. ***You cannot disable IPv4 support for your VPC and subnets since this is the default IP addressing system for Amazon VPC and Amazon EC2***.

By design, _each subnet must be associated with a network ACL_, which controls inbound and outbound traffic. Every subnet that you create is automatically associated with the default network ACL for the VPC. You can change the association, and you can change the contents of the default network ACL. 

https://docs.aws.amazon.com/vpc/latest/userguide/configure-subnets.html

### Subnet Sizing

#### IPv4

The first four IP addresses and the last IP address in each subnet CIDR block are not available for your use, and they cannot be assigned to a resource, such as an EC2 instance. For example, in a subnet with CIDR block 10.0.0.0/24, the following five IP addresses are reserved:
- 10.0.0.0: Network address.
- 10.0.0.1: Reserved by AWS for the VPC router.
- 10.0.0.2: Reserved by AWS. The IP address of the DNS server is the base of the VPC network range plus two. For VPCs with multiple CIDR blocks, the IP address of the DNS server is located in the primary CIDR. We also reserve the base of each subnet range plus two for all CIDR blocks in the VPC. For more information, see Amazon DNS server.
- 10.0.0.3: Reserved by AWS for future use.
- 10.0.0.255: Network broadcast address. We do not support broadcast in a VPC, therefore we reserve this address.

#### IPv6

The first four IPv6 addresses and the last IPv6 address in each subnet CIDR block are not available for your use, and they cannot be assigned to an EC2 instance. For example, in a subnet with CIDR block:
- 2001:db8:1234:1a00/64, the following five IP addresses are reserved:
- 2001:db8:1234:1a00::
- 2001:db8:1234:1a00::1: Reserved by AWS for the VPC router.
- 2001:db8:1234:1a00::2
- 2001:db8:1234:1a00::3
- 2001:db8:1234:1a00:ffff:ffff:ffff:ffff

In addition to the IP address reserved by AWS for the VPC router in the example above, the following IPv6 addresses are reserved for the default VPC router:
- A link-local IPv6 address in the FE80::/10 range generated using EUI-64. For more information about link-local addresses, see Link-local address.
- The link-local IPv6 address FE80:ec2::1.

If you need to communicate with the VPC router over IPv6, you can configure your applications to communicate with whichever address best fits your need.

## Intra/Inter communication

***By default, instances that you launch into a virtual private cloud (VPC) can’t communicate with your own network***. You can enable access to your network from your VPC by attaching a virtual private gateway to the VPC, creating a custom route table, updating your [security group](Security.md#security-groups) rules, and creating an AWS managed VPN connection.

Each subnet must be associated with a **route table**, which specifies the allowed routes for outbound traffic leaving the subnet. Every subnet that you create is automatically associated with the main route table for the VPC. You can change the association, and you can change the contents of the main route table.

Although the term VPN connection is a general term, *in the Amazon VPC documentation, a VPN connection refers to the connection between your VPC and your own network*. AWS supports Internet Protocol security (IPsec) VPN connections. A **customer gateway** is a physical device or software application on your side of the VPN connection. To create a VPN connection, ***you must create a customer gateway resource in AWS, which provides information to AWS about your customer gateway device***. Next, you have to set up an Internet-routable IP address (static) of the customer gateway’s external interface.

To check that two EC2 instances can communicate inside a VPC, first, the Network ACL should be properly set to allow communication between the two subnets. Second, the [security group](Security.md#security-groups) should also be properly configured so that your web server can communicate with the database server.

## Security Group vs Network Access Control List

| **Security Group** | **Network Access Control List** |
| --- | --- |
| Acts as a firewall for associated *EC2 instances* | Acts as a firewall for associated **subnets** |
| Controls both inbound and outbound traffic at the instance level | Controls both inbound and outbound traffic at the subnet level |
| You can secure your VPC instances using only SGs | Network ACLs are an additional layer of defense |
| Supports allow rules only | Supports allow and deny rules |
| **Stateful** (Return traffic is automatically allowed, regardless of any rules) | **Stateless** (Return traffic must be explicitly allowed by rules) |
| Evaluates all rules before deciding whether to allow traffic | Evaluates rules in number order when deciding whether to allow traffic, starting with the lowest numbered rule. |
| Applies only to the instance that is associated to it | Applies to all instances in the subnet it is associated with |
| Has separate rules for inbound and outbound traffic | <--- SAME |
| A newly created SG denies all inbound traffic by default | A newly created nACL denies all inbound traffic by default |
| A newly created SG has an outbound rule that *__allows__ all outbound traffic by default* | A newly created nACL denies all outbound traffic by default |
| Instances associated with a SG can't talk to each other unless you add rules allowing it | Each subnet in your VPC must be associated with a nACL. If none is associated, the default nACL is selected. |
| SGs are associated with network interfaces | You can associate a nACL with multiple subnets; however, a subnet can be associated with only one nACL at a time. |

## VPC Endpoint

A VPC endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by AWS PrivateLink without requiring an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection. ***Instances in your VPC do not require public IP addresses to communicate with resources in the service***. Traffic between your VPC and the other service does not leave the Amazon network.

When you create a VPC endpoint, ***you can attach an endpoint policy that controls access to the service to which you are connecting***. You can modify the endpoint policy attached to your endpoint and add or remove the route tables used by the endpoint. An endpoint policy does not override or replace IAM user policies or service-specific policies (such as S3 bucket policies). It is a separate policy for controlling access from the endpoint to the specified service. [^vpce]

There are two types of VPC endpoints and you should create the type of VPC endpoint required by the supported service: 
- **Interface endpoints** - Most AWS services use VPC Interface Endpoint, powered by [PrivateLink](#aws-privatelink) 
    - An interface endpoint is an ENI with a private IP address from the IP address range of your subnet
    - Unlike a Gateway endpoint, you still get billed for the time your interface endpoint is running and the GB data it has processed. 
- **Gateway endpoints**[^ge] - S3 and DynamoDB
    - A gateway endpoint is a gateway that is a target for a specified route in your route table, used for traffic destined to a supported AWS service.
    - Gateway endpoints provide reliable connectivity to Amazon S3 and DynamoDB without requiring an internet gateway or a NAT device for your VPC. Gateway endpoints do not enable AWS PrivateLink.

| Interface endpoints for S3 | Gateway endpoints for S3 |
| --- | --- |
| In both cases your network traffic remains on the AWS network | <--- |
| Use private IP from your VPC to access S3 | Use S3 public IP addresses |
| Allow access from on premises | Does not allow access from on premises |
| Allow access from a VPC in another AWS Region using VPC peering or AWS Transit Gatewat | Does not allow access from another AWS Region |
| Billed | Not billed |

[^ge]: [AWS docs Gateway Endpoints](https://docs.aws.amazon.com/vpc/latest/privatelink/gateway-endpoints.html)

### AWS PrivateLink

AWS PrivateLink[^pl] is a highly available, scalable technology that enables you to privately connect your VPC to services as if they were in your VPC. You do not need to use an internet gateway, NAT device, public IP address, AWS Direct Connect connection, or AWS Site-to-Site VPN connection to allow communication with the service from your private subnets. Therefore, you control the specific API endpoints, sites, and services that are reachable from your VPC.

[^pl]: [AWS docs PrivateLink](https://docs.aws.amazon.com/vpc/latest/privatelink/what-is-privatelink.html)

## NAT Gateway [^nat]

A NAT Gateway is a highly available, managed **Network Address Translation (NAT)** service for your resources in a *private subnet to access the Internet*. NAT gateway is created in a specific Availability Zone and implemented with redundancy in that zone.

***You must create a NAT gateway on a public subnet to enable instances in a private subnet to connect to the Internet or other AWS services, but prevent the Internet from initiating a connection with those instances.***

When you create a NAT gateway, you specify one of the following connectivity types:
- **Public** – (Default) *Instances in private subnets can connect to the internet through a public NAT gateway, but cannot receive unsolicited inbound connections from the internet*. You create a public NAT gateway in a public subnet and must associate an elastic IP address with the NAT gateway at creation. You route traffic from the NAT gateway to the internet gateway for the VPC. *Alternatively, you can use a public NAT gateway to connect to other VPCs or your on-premises network. In this case, you route traffic from the NAT gateway through a transit gateway or a virtual private gateway*.
- **Private** – *Instances in private subnets can connect to other VPCs or your on-premises network through a private NAT gateway*. You can route traffic from the NAT gateway through a transit gateway or a virtual private gateway. *You cannot associate an elastic IP address with a private NAT gateway*. You can attach an internet gateway to a VPC with a private NAT gateway, but if you route traffic from the private NAT gateway to the internet gateway, the internet gateway drops the traffic.

The NAT gateway replaces the source IP address of the instances with the IP address of the NAT gateway. For a public NAT gateway, this is the elastic IP address of the NAT gateway. For a private NAT gateway, this is the private IP address of the NAT gateway. When sending response traffic to the instances, the NAT device translates the addresses back to the original source IP address.

If you have resources in multiple Availability Zones and they share one NAT gateway, and if the NAT gateway’s Availability Zone is down, resources in the other Availability Zones lose Internet access. ***To create an Availability Zone-independent architecture, create a NAT gateway in each Availability Zone and configure your routing to ensure that resources use the NAT gateway in the same Availability Zone.***

An **egress-only internet gateway** is a horizontally scaled, redundant, and highly available VPC component that *allows outbound communication over IPv6 from instances in your VPC to the internet* and prevents it from initiating an IPv6 connection with your instances. *IPv6 addresses are globally unique and are therefore public by default*. If you want your instance to be able to access the internet, but you want to prevent resources on the internet from initiating communication with your instance, you can use an egress-only internet gateway. [^eo]

## Invalid Peering Configurations

Note that a VPC peering connection does not support edge to edge routing. This means that if either VPC in a peering relationship has one of the following connections, you cannot extend the peering relationship to that connection:
- A VPN connection or an AWS Direct Connect connection to a corporate network
- An Internet connection through an Internet gateway
- An Internet connection in a private subnet through a NAT device
- A gateway VPC endpoint to an AWS service; for example, an endpoint to Amazon S3.
- (IPv6) A ClassicLink connection. You can enable IPv4 communication between a linked EC2-Classic instance and instances in a VPC on the other side of a VPC peering connection. However, IPv6 is not supported in EC2-Classic, so you cannot extend this connection for IPv6 communication.

For example, if VPC A and VPC B are peered, and VPC A has any of these connections, then instances in VPC B cannot use the connection to access resources on the other side of the connection. Similarly, resources on the other side of a connection cannot use the connection to access VPC B.

## Network Firewall

AWS Network Firewall is a *stateful, managed network firewall and intrusion detection and prevention service for your virtual private cloud (VPC)* that you create in Amazon Virtual Private Cloud (Amazon VPC). With Network Firewall, you can filter traffic at the perimeter of your VPC. This includes filtering traffic going to and coming from an internet gateway, NAT gateway, or over VPN or AWS Direct Connect. Network Firewall uses the open source intrusion prevention system (IPS), Suricata, for stateful inspection. Network Firewall supports Suricata compatible rules. *AWS Network Firewall supports domain name stateful network traffic inspection*. You can create Allow lists and Deny lists with domain names that the stateful rules engine looks for in network traffic.

## Bastion Host

A bastion host is a special purpose computer on a network *specifically designed and configured to withstand attacks*. If you have a bastion host in AWS, **it is basically just an EC2 instance**. It should be in a **public subnet** with either a public or Elastic IP address with sufficient RDP or SSH access defined in the security group. Users log on to the bastion host via SSH or RDP and then use that session to manage other hosts in the private subnets.

## *Resources*

- [Tutorials Dojo VPC Cheat Sheet](https://tutorialsdojo.com/amazon-vpc/)

[^vpce]: [AWS VPC Endpoints docs](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints-s3.html)
[^nat]: [AWS NAT Gateway docs](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html)
[^eo]: [AWS Egress-only Internet Gateway docs](https://docs.aws.amazon.com/vpc/latest/userguide/egress-only-internet-gateway.html)