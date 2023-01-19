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

### ALB w/Lambda

Application Load Balancers provide two advanced options that you may want to configure when you use ALBs with AWS Lambda: support for multi-value headers and health check configurations. You can set up these options in Target Groups section on the Amazon EC2 console.

If requests from a client or responses from a Lambda function contain headers with multiple values or contains the same header multiple times, or query parameters with multiple values for the same key, you can enable support for multi-value header syntax. After you enable multi-value headers, the headers and query parameters exchanged between the load balancer and the Lambda function use arrays instead of strings.

For example, suppose the client supplies a query string like:
```
?name=foo&name=bar
```
If you’ve enabled multi-value headers, ALB supplies these duplicate parameters in the event object as:
```
‘name’: [‘foo’, ‘bar’]
```
ALB applies the same processing to duplicate HTTP headers.

If you do not enable multi-value header syntax and a header or query parameter has multiple values, the load balancer uses the last value that it receives.
https://aws.amazon.com/blogs/networking-and-content-delivery/lambda-functions-as-targets-for-application-load-balancers/

## *Resources*

- [Tutorials Dojo ELB Cheat Sheet](https://tutorialsdojo.com/aws-elastic-load-balancing-elb/)