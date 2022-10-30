# CloudFront

Amazon CloudFront is a fast **content delivery network (CDN) service** that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds, all within a developer-friendly environment. CloudFront is integrated with AWS – both physical locations that are directly connected to the AWS global infrastructure, as well as other AWS services and works seamlessly with services, including AWS Shield for DDoS mitigation.

## Origin Failover

CloudFront also allows you to set up multiple origins to *enable redundancy with Origin Failover*. To set up origin failover, you must have a distribution with at least two origins. Next, *you create an origin group for your distribution that includes the two origins*, ***setting one as the primary***. Finally, you define a cache behavior in which you specify the origin group as your origin.

The two origins in the origin group can be any combination of the following: AWS origins, like Amazon S3 buckets or Amazon EC2 instances, or custom origins, like your own HTTP web server. When you create the origin group, you configure CloudFront to failover to the second origin for GET, HEAD, and OPTIONS HTTP methods when the primary origin returns specific status codes that you configure.


## *Resources*

- [Origin failover AWS docs](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/high_availability_origin_failover.html)