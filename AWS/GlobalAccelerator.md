# Global Accelerator

Global Accelerator improves performance for a wide range of applications over TCP or UDP by proxying packets at the edge to applications running in one or more AWS Regions. Global Accelerator is a good fit for non-HTTP use cases, such as gaming (UDP), IoT (MQTT), or Voice over IP, as well as for HTTP use cases that specifically require static IP addresses or deterministic, fast regional failover. Like CloudFront, Global Accelerator uses the AWS global network and its edge locations around the world

It provides static IP addresses that act as a fixed entry point to your application endpoints in a single or multiple AWS Regions, such as your Application Load Balancers, Network Load Balancers or Amazon EC2 instances.

AWS Global Accelerator continually monitors the health of your application endpoints and will detect an unhealthy endpoint and redirect traffic to healthy endpoints in less than 1 minute.

## Concepts

- An **accelerator** is the resource you create to direct traffic to optimal endpoints over the AWS global network.
- **Network zones** are isolated units with their own set of physical infrastructure and service IP addresses from a unique IP subnet.
- AWS Global Accelerator provides you with a set of **two static IP addresses **that are anycast from the AWS edge network. It also assigns a default Domain Name System (DNS) name to your accelerator, similar to a1234567890abcdef.awsglobalaccelerator.com, that points to the static IP addresses.
- A **listener** processes inbound connections from clients to Global Accelerator, based on the port (or port range) and protocol that you configure. Global Accelerator supports both TCP and UDP protocols.
- Each **endpoint group** is associated with a specific AWS Region. Endpoint groups include one or more endpoints in the Region.
- **Endpoints** can be Network Load Balancers, Application Load Balancers, EC2 instances, or Elastic IP addresses.

## Global Accelerator vs. CloudFront

| **Global Accelerator** | **CloudFront** |
| --- | --- |
| Improves performance for a wide range of applications over TCP or UDP by proxying packets at the edge to applications running in one or more AWS Regions. | Improves performance for both cacheable content(such as images and videos) and dynamic content (such as API acceleration and dynamic site delivery) |
| Good fit for non-HTTP use cases, such as gaming (UDP), IoT (MQTT), or VoIP, as well as for HTTP use cases that specifically require static IP addresses or deterministic, fast regional failover. | Best used for HTTP use cases, as well as securing access over your endpoints (S3, ELB, EC2). Also offers several options for streaming your media to global viewers -both pre-recorded files and live events. Lastly, using Lamda@Edge can help you configure your CloudFront distribution to serve private content from your own custom origin, as an option to using signed URLs or signed cookies. | 

## *Resources*

- [AWS Docs Global Accelerator](https://aws.amazon.com/global-accelerator/)
- [Tutorials Dojo Global Accelerator Cheat Sheet](https://tutorialsdojo.com/aws-global-accelerator/)
