# AWS WAF

AWS WAF is a **web application firewall** that lets you monitor the HTTP and HTTPS requests that are forwarded to an Amazon API Gateway API, Amazon CloudFront or an Application Load Balancer. WAF helps protect your web applications or APIs against common web exploits that may affect availability, compromise security, or consume excessive resources. *AWS WAF gives you control over how traffic reaches your applications by enabling you to create security rules that block common attack patterns, such as SQL injection or cross-site scripting, and rules that filter out specific traffic patterns you define*. 

AWS WAF is easy to deploy and protect applications deployed on the following services:
- Amazon CloudFront as part of your CDN solution
- Application Load Balancer that fronts all your origin servers
- Amazon API Gateway for your REST APIs
- AWS AppSync for your GraphQL APIs. 

There is no additional software to deploy, DNS configuration, SSL/TLS certificate to manage, or need for a reverse proxy setup.

- You define your conditions, combine your conditions into rules, and combine the rules into a **web ACL**.
    - This is where you define an action for each rule— [allow, block, or count](#web-acl)— and a default action, which determines whether to allow or block a request that doesn’t match all the conditions in any of the rules in the web ACL.
- **Conditions** define the basic characteristics that you want WAF to watch for in web requests.
- You combine conditions into **rules** to precisely target the requests that you want to allow, block, or count. WAF provides two types of rules:
    - **Regular rules** – use only conditions to target specific requests.
    - **Rate-based rules** – are similar to regular rules, with a rate limit. Rate-based rules count the requests that arrive from a specified IP address every five minutes. The rule can trigger an action if the number of requests exceed the rate limit. The following are customized rate-based rules for application protection:
        - **Blanket rate-based rule**: Prevents source IP address from making excessive requests to entire applications.
        - **URI-specific rate-based rule**: Prevents IP address from making excessive requests to the URI (Uniform Request Identifier) of the application. _These are useful if specific functions of the applications, such as computationally expensive resources need to be protected from excessive requests_.
        - **IP reputation rate-based rule**: Prevents _well-known malicious IP addresses_ from making excessive requests to the application.

**WAF Managed Rules** are an easy way to deploy pre-configured rules to protect your applications common threats like application vulnerabilities. All Managed Rules are automatically updated by AWS Marketplace security Sellers.

You can insert HTTP headers to a user request when WAF allows the request to reach your application. You can use the custom HTTP headers to validate the requests made to your application passed through WAF, and configure your application to only allow requests that contain the custom header values that you specify. You can also insert headers so your application can process the request differently based on the presence of the header, or log the header in your application logs for reporting and analytics.

WAF lets you configure the HTTP status code and the response body returned to the user when a request is blocked. _Based on conditions that you specify, such as the IP addresses that requests originate from or the values of query strings_, API Gateway, CloudFront or an Application Load Balancer responds to requests either with the requested content or with an HTTP 403 status code (Forbidden). You also can configure CloudFront to return a custom error page when a request is blocked.

## Web ACL

At the simplest level, AWS WAF lets you choose one of the following behaviors:
- **Allow all requests except the ones that you specify** – This is useful when you want CloudFront or an Application Load Balancer to serve content for a public website, but you also want to block requests from attackers.
- **Block all requests except the ones that you specify** – This is useful when you want to serve content for a restricted website whose users are readily identifiable by properties in web requests, such as the IP addresses that they use to browse to the website.
- **Count the requests that match the properties that you specify** – When you want to allow or block requests based on new properties in web requests, you first can configure AWS WAF to count the requests that match those properties without allowing or blocking those requests. This lets you confirm that you didn’t accidentally configure AWS WAF to block all the traffic to your website. When you’re confident that you specified the correct properties, you can change the behavior to allow or block requests.

# AWS Shield/Shield Advanced

Shield is a managed Distributed Denial of Service (DDoS) protection service that safeguards applications running on AWS. All AWS customers benefit from the automatic protections of Shield Standard. Shield Standard provides always-on network flow monitoring which inspects incoming traffic to AWS and detect malicious traffic in real-time.
Shield uses several techniques like deterministic packet filtering, and priority based traffic shaping to automatically mitigate attacks without impact to your applications.

When you use Shield Standard with CloudFront and Route 53, you receive comprehensive availability protection against all known infrastructure attacks. You can also view all the events detected and mitigated by AWS Shield in your account.

For higher levels of protection against attacks targeting your applications running on Amazon Elastic Compute Cloud (EC2), Elastic Load Balancing(ELB), Amazon CloudFront, and Amazon Route 53 resources, you can subscribe to **AWS Shield Advanced**. In addition to the network and transport layer protections that come with Standard, AWS Shield Advanced provides _additional detection and mitigation against large and sophisticated DDoS attacks, near real-time visibility into attacks, and integration with AWS WAF, a web application firewall_.

AWS Shield Advanced also gives you 24×7 access to the AWS DDoS Response Team (DRT) and protection against DDoS related spikes in your Amazon Elastic Compute Cloud (EC2), Elastic Load Balancing(ELB), Amazon CloudFront, and Amazon Route 53 charges.


**AWS Firewall Manager** just simplifies your AWS WAF and AWS Shield Advanced administration and maintenance tasks across multiple accounts and resources.