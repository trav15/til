# Certificate Manager

A service that lets you easily provision, manage, and deploy public and private SSL/TLS certificates for use with AWS services and your internal connected resources. SSL/TLS certificates are used to secure network communications and establish the identity of websites over the Internet as well as resources on private networks.

ACM is integrated with the following services:
- Elastic Load Balancing
- Amazon CloudFront – To use an ACM certificate with CloudFront, you must request or import the certificate in the US East (N. Virginia) region.
- AWS Elastic Beanstalk
- Amazon API Gateway
- AWS CloudFormation

AWS Certificate Manager manages the renewal process for the certificates managed in ACM and used with ACM-integrated services. *You can import your own certificates into ACM, however you have to renew these yourself*.

To use an ACM certificate with Amazon CloudFront, you must request or import the certificate in the US East (N. Virginia) region. ACM certificates in this region that are associated with a CloudFront distribution are distributed to all the geographic locations configured for that distribution.

ACM Certificate are X.509 version 3 certificates. Each is valid for 13 months. Each ACM Certificate must include at least one **fully qualified domain name (FQDN)**. You can add additional names if you want to.

The first time you request or import a certificate in an AWS region, ACM creates an AWS-managed customer master key (CMK) in AWS KMS with the alias aws/acm. This CMK is unique in each AWS account and each AWS region. ACM uses this CMK to encrypt the certificate’s private key.

## *Resources*

- [AWS Certificate Manager docs](https://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html)