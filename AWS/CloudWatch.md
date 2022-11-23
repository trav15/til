# CloudWatch

CloudWatch collects monitoring and operational data in the form of logs, metrics, and events, providing you with a unified view of AWS resources, applications, and services that run on AWS, and on-premises servers.

Amazon CloudWatch has available Amazon EC2 Metrics for you to use for monitoring:
- CPU utilization
- Network utilization
- Disk performance
- Disk Reads/Writes. 

The below items require you to prepare a **custom metric** using a Perl or other shell script, as there are no ready to use metrics for:
- Memory utilization
- Disk swap utilization
- Disk space utilization
- Page file utilization
- Log collection

***To monitor custom metrics, you must install the CloudWatch agent on the EC2 instance***. After installing the CloudWatch agent, you can now collect system metrics and log files of an EC2 instance.

## Amazon EventBridge

Amazon EventBridge (formerly called CloudWatch Events)[^eb] is a **serverless event bus** that makes it easy to connect applications together. It uses data from your own applications, integrated software as a service (SaaS) applications, and AWS services. This simplifies the process of building event-driven architectures by decoupling event producers from event consumers. This allows producers and consumers to be scaled, updated, and deployed independently. Loose coupling improves developer agility in addition to application resiliency.

You can use Amazon EventBridge to run Amazon ECS tasks when certain AWS events occur. Amazon EventBridge can be used to build applications that start processing after any changes to the objects stored in Amazon S3 buckets. All Amazon S3 event notifications are directly sent to Amazon EventBridge in a reliable and quick way. Amazon EventBridge provides additional benefits such as:
- Advance Filtering: This helps to match object parameters which can be used to get only specific notifications.
- Multiple Destinations: Amazon EventBridge can be used forward event notifications to multiple destinations.
- Fast, Reliable Invocation: Amazon EventBridge provides a fast and reliable way to forward notifications without additional custom codes. 

[^eb]: https://aws.amazon.com/blogs/aws/new-use-amazon-s3-event-notifications-with-amazon-eventbridge/

## *Resources*

- [Tutorials Dojo CloudWatch Cheat Sheet](https://tutorialsdojo.com/amazon-cloudwatch/)