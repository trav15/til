# CloudFront

Amazon CloudFront is a fast **content delivery network (CDN) service** that securely delivers data, videos, applications, and APIs to customers globally with low latency, high transfer speeds, all within a developer-friendly environment. CloudFront is integrated with AWS – both physical locations that are directly connected to the AWS global infrastructure, as well as other AWS services and works seamlessly with services, including AWS Shield for DDoS mitigation.

CloudFront delivers your content through a worldwide network of data centers called **edge locations**. When a user requests content that you’re serving with CloudFront, _the user is routed to the edge location that provides the lowest latency_, so that content is delivered with the best possible performance.
- If the content is already in the edge location with the lowest latency, CloudFront delivers it immediately.
- If the content is not in that edge location, CloudFront retrieves it from an origin that you’ve defined

## How CloudFront Delivers Content

You specify **origin servers**, like an S3 bucket or your own HTTP server, from which CloudFront gets your files which will then be distributed from CloudFront edge locations all over the world.
- Upload your files to your origin servers. Your files are also known as **objects**.
- Create a **CloudFront distribution**, which tells CloudFront which origin servers to get your files from when users request the files through your web site or application. At the same time, you specify details such as whether you want CloudFront to log all requests and whether you want the distribution to be enabled as soon as it’s created.
- CloudFront assigns a domain name to your new distribution that you can see in the CloudFront console.
- CloudFront sends your distribution’s configuration (but not your content) to all of its edge locations—collections of servers in geographically dispersed data centers where CloudFront caches copies of your objects.

## CloudFront Origins

- **Using S3 buckets for your origin** – you place any objects that you want CloudFront to deliver in an S3 bucket.
- **Using S3 buckets configured as website endpoints** for your origin
- **Using a mediastore container or a media package channel** for your origin – you can set up an S3 bucket that is configured as a MediaStore container, or create a channel and endpoints with MediaPackage. Then you create and configure a distribution in CloudFront to stream the video.
- **Using an Application Load Balancer** – if your origin is more than one HTTP server, you can use an ALB to distribute traffic to the web servers.
- **Using a Lambda function URL** – you don’t need to use an API Gateway or ALB since a Lambda web application can be called directly from the function URL.
- **Using EC2 or other custom origins** – A custom origin is an HTTP server, for example, a web server.
- **Using CloudFront Origin Groups for origin failover** – use **[origin failover](#origin-failover)** to designate a primary origin for CloudFront plus a second origin that CloudFront automatically switches to when the primary origin returns specific HTTP status code failure responses.

## Cache Headers

The `Cache-Control` and `Expires` headers control how long objects stay in the cache. The `Cache-Control max-age` directive lets you specify how long (in seconds) you want an object to remain in the cache before CloudFront gets the object again from the origin server. Typically, CloudFront serves an object from an edge location until the cache duration that you specified passes — that is, until the object expires. After it expires, the next time the edge location gets a user request for the object, CloudFront forwards the request to the origin server to verify that the cache contains the latest version of the object. The minimum expiration time CloudFront supports is 0 seconds for web distributions and 3600 seconds for RTMP distributions. *If the max-age directive is set to zero then the request is always directed to the origin server.*

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
- [Tutorials Dojo CloudFront Cheat Sheet](https://tutorialsdojo.com/amazon-cloudfront/)