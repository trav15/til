# Lambda

***AWS Lambda supports resource-based permissions policies for Lambda functions and layers***. Lambda will automatically track the behavior of your Lambda function invocations and provide feedback that you can monitor. In addition, it provides metrics that allows you to analyze the full function invocation spectrum, including event source integration and whether downstream resources perform as expected.

Resource-based policies let you *grant usage permission to other AWS accounts on a per-resource basis*. You also use a resource-based policy to allow an AWS service to invoke your function on your behalf.

For Lambda functions, *you can grant account permission to invoke or manage a function*. You can add multiple statements to grant access to several accounts, or let any account invoke your function. You can also use the policy to grant invoke permission to an AWS service that invokes a function in response to activity in your account. 

_**Execution roles** grant Lambda functions access to other AWS services_. You can’t use it to control which entity can invoke the function. IAM roles, in general, do not support the principal element.

AWS Lambda *supports the synchronous and asynchronous invocation of a Lambda function*. You can control the invocation type only when you invoke a Lambda function. When you use an AWS service as a trigger, the invocation type is predetermined for each service. You have no control over the invocation type that these event sources use when they invoke your Lambda function. Since processing only takes 5 minutes, Lambda is also a cost-effective choice.

*Lambda can scale faster than the regular Auto Scaling feature of Amazon EC2, Amazon Elastic Beanstalk, or Amazon ECS*. This is because AWS Lambda is more lightweight than other computing services. Under the hood, Lambda can run your code to thousands of available AWS-managed EC2 instances (that could already be running) within seconds to accommodate traffic. This is faster than the Auto Scaling process of launching new EC2 instances that could take a few minutes or so. An alternative is to overprovision your compute capacity but that will incur significant costs. 

When you create or update Lambda functions that use environment variables, *AWS Lambda encrypts them using the AWS Key Management Service*. When your Lambda function is invoked, those values are decrypted and made available to the Lambda code. The first time you create or update Lambda functions that use environment variables in a region, a *default service key is created for you automatically within AWS KMS*. This key is used to encrypt environment variables. However, _if you wish to use **encryption helpers** and use KMS to encrypt environment variables after your Lambda function is created, you must create your own AWS KMS key and choose it instead of the default key_. The default key will give errors when chosen. Creating your own key gives you more flexibility, including the ability to create, rotate, disable, and define access controls, and to audit the encryption keys used to protect your data.

## Lambda Throttling

Lambda Throttling refers to the rejection of the Lambda function to invocation requests. At this event, the Lambda will return a throttling error exception which you need to handle. This happens because your current concurrency execution count is greater than your concurrency limit.
Throttling is intended to protect your resources and downstream applications. Though Lambda automatically scales to accommodate your incoming traffic, your function can still be throttled for various reasons.

The following are the recommended solutions to handle throttling issues:
- Configure **reserved concurrency** – by default, there are 900 unreserved concurrencies shared across all functions in a region. To prevent other functions from consuming the available concurrent executions, reserve a portion of it to your Lambda function based on the demand of your current workload.
- Use **exponential backoff** in your app – a technique that uses progressively longer waits between retries for consecutive error responses. This can be used to handle throttling issues by preventing collision between simultaneous requests.
- Use a **dead-letter queue** – If you’re using Amazon S3 and Amazon Cloudwatch events, configure your function with a dead letter queue to catch any events that are discarded due to constant throttles. This can protect your data if you’re seeing significant throttling.
- Request a **service quota increase** – you can reach AWS support to request for a higher service quota for concurrent executions.

## Lambda@Edge

Lambda@Edge lets you _run Lambda functions to customize the content that CloudFront delivers_, executing the functions in AWS locations closer to the viewer. The functions run in response to CloudFront events, without provisioning or managing servers. You can _use Lambda functions to change CloudFront requests and responses_ at the following points:
- After CloudFront receives a request from a viewer (viewer request)
- Before CloudFront forwards the request to the origin (origin request)
- After CloudFront receives the response from the origin (origin response)
- Before CloudFront forwards the response to the viewer (viewer response)


## *Resources*

- [Tutorials Dojo Lambda Cheat Sheet](https://tutorialsdojo.com/aws-lambda/)
- [AWS Lambda Env Variables docs](https://docs.aws.amazon.com/lambda/latest/dg/configuration-envvars.html#env_encrypt)
- https://aws.amazon.com/premiumsupport/knowledge-center/lambda-troubleshoot-throttling/
- https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html