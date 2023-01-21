# AWS X-Ray

AWS X-Ray analyzes and debugs production, distributed applications, such as those built using a microservices architecture. With X-Ray, you can identify performance bottlenecks, edge case errors, and other hard to detect issues.

AWS X-Ray can be used with applications running on Amazon EC2, Amazon ECS, AWS Lambda, AWS Elastic Beanstalk. You just integrate the X-Ray SDK with your application and install the X-Ray agent.

AWS X-Ray provides an end-to-end, cross-service, application-centric view of requests flowing through your application by aggregating the data gathered from individual services in your application into a single unit called a trace.

## Segments & Subsegments

A **segment** provides the name of the compute resources running your application logic, details about the request sent by your application, and details about the work done.

A segment can break down the data about the work done into **subsegments**. A subsegment can contain additional details about a call to an AWS service, an external HTTP API, or an SQL database.

For services that don’t send their own segments, like Amazon DynamoDB, X-Ray uses subsegments to generate inferred segments and downstream nodes on the service map. This lets you see all of your downstream dependencies, even if they don’t support tracing, or are external.

Subsegments represent your application’s view of a downstream call as a client. If the downstream service is also instrumented (like an AWS SDK client), the segment that it sends replaces the inferred segment generated from the upstream client’s subsegment.

X-Ray uses the data that your application sends to generate a service graph. Each AWS resource that sends data to X-Ray appears as a service in the graph

## Service Graph

A service graph is a JSON document that contains information about the services and resources that make up your application. The X-Ray console uses the service graph to generate a visualization or service map. Service graph data is retained for 30 days.

## Edges

Edges connect the services that work together to serve requests. Edges connect clients to your application, and your application to the downstream services and resources that it uses.

## *Resources*