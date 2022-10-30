# CloudFront

Amazon CloudFront is a fast **content delivery network (CDN) service** that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds, all within a developer-friendly environment. CloudFront is integrated with AWS – both physical locations that are directly connected to the AWS global infrastructure, as well as other AWS services and works seamlessly with services, including AWS Shield for DDoS mitigation.

## Origin Failover

CloudFront also allows you to set up multiple origins to *enable redundancy with Origin Failover*. To set up origin failover, you must have a distribution with at least two origins. Next, *you create an origin group for your distribution that includes the two origins*, ***setting one as the primary***. Finally, you define a cache behavior in which you specify the origin group as your origin.

The two origins in the origin group can be any combination of the following: AWS origins, like Amazon S3 buckets or Amazon EC2 instances, or custom origins, like your own HTTP web server. When you create the origin group, you configure CloudFront to failover to the second origin for GET, HEAD, and OPTIONS HTTP methods when the primary origin returns specific status codes that you configure.

## Signed URLs and Signed Cookies

To securely serve this private content by using CloudFront, you can do the following:
- Require that your users access your private content by using special CloudFront **signed URLs** or **signed cookies**.
- Require that your users access your content by using **CloudFront URLs**, not URLs that access content directly on the origin server (for example, Amazon S3 or a private HTTP server). *Requiring CloudFront URLs isn’t necessary, but we recommend it to prevent users from bypassing the restrictions* that you specify in signed URLs or signed cookies.

CloudFront signed URLs and signed cookies provide the same basic functionality: they allow you to control who can access your content
- Use signed URLs for the following cases:
    - You want to use an RTMP distribution. Signed cookies aren’t supported for RTMP distributions.
    - You want to restrict access to individual files, for example, an installation download for your application.
    - Your users are using a client (for example, a custom HTTP client) that doesn’t support cookies.
- Use signed cookies for the following cases:
    - You want to provide access to multiple restricted files, for example, all of the files for a video in HLS format or all of the files in the subscribers’ area of a website.
    - You don’t want to change your current URLs.

## *Resources*

- [Origin failover AWS docs](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/high_availability_origin_failover.html)
- [Private content AWS docs](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-choosing-signed-urls-cookies.html)