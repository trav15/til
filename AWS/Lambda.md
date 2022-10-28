# Lambda

***AWS Lambda supports resource-based permissions policies for Lambda functions and layers***. Lambda will automatically track the behavior of your Lambda function invocations and provide feedback that you can monitor. In addition, it provides metrics that allows you to analyze the full function invocation spectrum, including event source integration and whether downstream resources perform as expected.

Resource-based policies let you *grant usage permission to other AWS accounts on a per-resource basis*. You also use a resource-based policy to allow an AWS service to invoke your function on your behalf.

For Lambda functions, *you can grant account permission to invoke or manage a function*. You can add multiple statements to grant access to several accounts, or let any account invoke your function. You can also use the policy to grant invoke permission to an AWS service that invokes a function in response to activity in your account. 

_**Execution roles** grant Lambda functions access to other AWS services_. You can’t use it to control which entity can invoke the function. IAM roles, in general, do not support the principal element.

AWS Lambda *supports the synchronous and asynchronous invocation of a Lambda function*. You can control the invocation type only when you invoke a Lambda function. When you use an AWS service as a trigger, the invocation type is predetermined for each service. You have no control over the invocation type that these event sources use when they invoke your Lambda function. Since processing only takes 5 minutes, Lambda is also a cost-effective choice.

*Lambda can scale faster than the regular Auto Scaling feature of Amazon EC2, Amazon Elastic Beanstalk, or Amazon ECS*. This is because AWS Lambda is more lightweight than other computing services. Under the hood, Lambda can run your code to thousands of available AWS-managed EC2 instances (that could already be running) within seconds to accommodate traffic. This is faster than the Auto Scaling process of launching new EC2 instances that could take a few minutes or so. An alternative is to overprovision your compute capacity but that will incur significant costs. 