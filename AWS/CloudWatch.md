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

## *Resources*

- [Tutorials Dojo CloudWatch Cheat Sheet](https://tutorialsdojo.com/amazon-cloudwatch/)