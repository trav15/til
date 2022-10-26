# ELB

Components:
- A load balancer serves as the single point of contact for clients.
- A listener checks for connection requests from clients. You must define a default rule for each listener that specifies a target group, condition, and priority.
- Target group routes requests to one or more registered targets. You can register a target with multiple target groups, and configure health checks on a per target group basis.

## Network Load Balancer

A Network Load Balancer functions at the **layer 4** of the Open Systems Interconnection (OSI) model. *It can handle millions of requests per second*. After the load balancer receives a connection request, it selects a target from the default rule’s target group. It attempts to open a TCP connection to the selected target on the port specified in the listener configuration.

At least 1 subnet must be specified when creating this type of load balancer, but the recommended number is 2. *Network Load Balancers do not support gRPC*.

## Application Load Balancer

ALB functions at the application layer, **layer 7** of the Open Systems Interconnection (OSI) model. Ideal for advanced load balancing of HTTP and HTTPS traffic, ALB provides advanced request routing targeted at delivery of modern application architectures, including microservices and container-based applications. ALB simplifies and improves the security of your application, by ensuring that the latest SSL/TLS ciphers and protocols are used at all times.

At least 2 subnets must be specified when creating this type of load balancer. *Support for path-based and host-based routing*.

*You can’t assign an Elastic IP address to an Application Load Balancer*. The alternative method you can do is assign an Elastic IP address to a Network Load Balancer in front of the ALB.

***ALBs can also route and load balance gRPC traffic between microservices or between gRPC-enabled clients and services***. This will allow customers to seamlessly introduce gRPC traffic management in their architectures without changing any of the underlying infrastructure on their clients or services.