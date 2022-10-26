# Security

A **defense-in-depth strategy** is one of the design principles for security in the AWS cloud. This strategy entails *implementing security controls at multiple layers* (for example, edge of network, VPC, load balancing, every instance and compute service, operating system, application, and code).

Components such as EC2 instances, RDS database clusters, and Lambda functions that share reachability requirements **can be segmented into layers formed by subnets**. For example, an RDS database cluster in a VPC with no need for internet access should be placed in subnets with no route to or from the internet. *This layered approach for the controls mitigates the impact of a single layer misconfiguration, which could allow unintended access*.
