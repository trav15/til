# Route 53

A highly available and scalable Domain Name System (DNS) web service used for domain registration, DNS routing, and health checking. You can create a new Route 53 with the failover option to a static S3 website bucket or CloudFront distribution as an alternative.

*To route domain traffic to an ELB load balancer, use Amazon Route 53 to create an alias record that points to your load balancer*. An alias record is a Route 53 extension to DNS. It’s similar to a CNAME record, but you can create an alias record both for the root domain, such as example.com and for subdomains, such as portal.example.com. (You can create CNAME records only for subdomains.) 

To enable IPv6 resolution, you would need to create a second resource record, example.com ALIAS AAAA -> myelb.us-west-2.elb.amazonnaws.com, this is assuming your Elastic Load Balancer has IPv6 support.

When responding to queries, *Route 53 includes only the healthy primary resources*. If all the primary resources are unhealthy, Route 53 begins to include only the healthy secondary resources in response to DNS queries. To create an active-passive failover configuration with one primary record and one secondary record, you just create the records and specify **Failover** for the routing policy. 

When Route 53 checks the health of an endpoint, it sends an HTTP, HTTPS, or TCP request to the IP address and port that you specified when you created the health check. ***For a health check to succeed, your router and firewall rules must allow inbound traffic from the IP addresses that the Route 53 health checkers use***.

## Active-Passive Failover

Amazon Route 53 health checks can be used to configure active-active and active-passive failover configurations. **Active-passive failover** configuration can be used when primary resources are available most of the time, and secondary resources are used only in case of primary resources are not available.

For configuring active-passive failover with multiple primary and secondary resources, the following setting can be done:
- For Primary resources, create an alias record pointing to Application Load Balancer with `evaluate health check` as yes.
- For Secondary resources, create health checks for the web servers in the data centers.
- Create two failover alias records, one for primary and one for secondary resources.

## *Resources*

- [Tutorials Dojo Route 53 Cheat Sheet](https://tutorialsdojo.com/amazon-route-53/)