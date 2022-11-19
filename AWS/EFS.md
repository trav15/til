# Amazon Elastic File System (EFS)

Amazon Elastic File System (EFS) is a fully-managed _file storage service_ that provides simple, scalable, elastic file storage for use with AWS Cloud services and on-premises resources. When mounted on Amazon EC2 instances, an Amazon EFS file system provides a standard file system interface and file system access semantics, allowing you to _seamlessly integrate Amazon EFS with your existing applications and tools_. Multiple Amazon EC2 instances can access an Amazon EFS file system at the same time, allowing Amazon EFS to provide a _common data source for workloads and applications running on more than one Amazon EC2 instance_.

## Amazon FSx for Lustre

Amazon FSx For Lustre is a high-performance file system for fast processing of workloads. Lustre is a popular **open-source parallel file system** which stores data across multiple network file servers to maximize performance and reduce bottlenecks. _Important for AI and machine learning_. Since this is a high-performance parallel file system, you can use Amazon FSx as “hot” storage for your highly accessed files, and Amazon S3 as “cold” storage for rarely accessed files.

## *Resources*

- [Tutorials Dojo EFS Cheat Sheet](https://tutorialsdojo.com/amazon-efs/)