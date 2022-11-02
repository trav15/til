# CloudTrail

AWS CloudTrail is a service that _enables governance, compliance, operational auditing, and risk auditing of your AWS account_. With CloudTrail, you can **log**, continuously monitor, and retain account activity related to actions across your AWS infrastructure. _By default, CloudTrail is enabled on your AWS account when you create it_. When activity occurs in your AWS account, that activity is recorded in a CloudTrail event. You can easily view recent events in the CloudTrail console by going to **Event history**.

CloudTrail events provide a history of both API and non-API account activity made through the AWS Management Console, AWS SDKs, command-line tools, and other AWS services. There are two types of events that can be logged in CloudTrail: **management events** and **data events**. _By default, CloudTrail logs management events, but not data events_.

_A trail can be applied to all regions or a single _region_. As a best practice, create a trail that applies to all regions in the AWS partition in which you are working. This is the default setting when you create a trail in the CloudTrail console.

_For most services, events are recorded in the region where the action occurred_. For global services such as AWS Identity and Access Management (IAM), AWS STS, Amazon CloudFront, and Route 53, events are delivered to any trail that includes global services, and are logged as occurring in US East (N. Virginia) Region. In order to log global services in a multi-region trail, you have to add the `--include-global-service-events` parameter in your AWS CLI command.

## _Resources_
- [Tutorials Dojo CloudTrail Cheat Sheet](https://tutorialsdojo.com/aws-cloudtrail/)