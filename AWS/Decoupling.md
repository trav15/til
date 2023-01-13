# Decoupling

Decoupled architecture is a type of computing architecture that enables computing components or layers to execute independently while still interfacing with each other.
Amazon Simple Queue Service (SQS) and Amazon Simple Workflow Service (SWF) are the services that you can use for creating a decoupled architecture in AWS. Amazon SQS lets you move data between distributed application components and helps you decouple these components. 

## Amazon EventBridge

Amazon EventBridge (formerly called CloudWatch Events) is a ***serverless event bus*** that makes it easy to connect applications together. It uses data from your own applications, integrated software as a service (SaaS) applications, and AWS services. This simplifies the process of building event-driven architectures by decoupling event producers from event consumers. This allows producers and consumers to be scaled, updated, and deployed independently. Loose coupling improves developer agility in addition to application resiliency.

You can use Amazon EventBridge to run Amazon ECS tasks when certain AWS events occur. Amazon EventBridge can be used to build applications that start processing after any changes to the objects stored in Amazon S3 buckets. All Amazon S3 event notifications are directly sent to Amazon EventBridge in a reliable and quick way[^event]. Amazon EventBridge provides additional benefits such as:
- Advance Filtering: This helps to match object parameters which can be used to get only specific notifications.
- Multiple Destinations: Amazon EventBridge can be used forward event notifications to multiple destinations.
- Fast, Reliable Invocation: Amazon EventBridge provides a fast and reliable way to forward notifications without additional custom codes. 

[^event]: https://aws.amazon.com/blogs/aws/new-use-amazon-s3-event-notifications-with-amazon-eventbridge/


## Amazon Simple Workflow Service (SWF)

SWF is a web service that makes it easy to coordinate work across distributed application components. In Amazon SWF, tasks represent invocations of logical steps in applications. Tasks are processed by workers which are programs that interact with Amazon SWF to get tasks, process them, and return their results. ***With Amazon SWF, you write a decider program to separate activity steps from decision steps***. This provides you complete control over your orchestration logic, but increases the complexity of developing applications. ***You may write decider programs in the programming language of your choice***, or you may use the **Flow framework**, which is a library for building SWF applications.

## AWS Step Functions 

Step Functions is a fully managed service that makes it easy to coordinate the components of distributed applications and microservices using **visual workflows**. You define **state machines** that describe your workflow as a series of steps, their relationships, and their inputs and outputs. State machines contain a number of **states**, *each of which represents an individual step in a workflow diagram*. States can perform work, make choices, pass parameters, initiate parallel execution, manage timeouts, or terminate your workflow with a success or failure. ***With Step Functions, you write state machines in declarative JSON***. Step Functions keeps track of all tasks and events in an application. You can use Amazon SQS to build basic workflows to coordinate your distributed application, but you get this facility out-of-the-box with Step Functions, alongside other application-level capabilities.

Step Functions automatically triggers and tracks each step, and retries when there are errors so your application executes in order and as expected. With Step Functions, you can craft long-running workflows such as machine learning model training, report generation, and IT automation. You can manage the coordination of a state machine in Step Functions using the Amazon States Language. The **Amazon States Language** is a JSON-based, structured language used to define your state machine, a collection of states, that can do work (**Task states**), determine which states to transition to next (**Choice states**), stop execution with an error (**Fail states**), and so on.

## *Resources* 

### Step Functions

- https://tutorialsdojo.com/aws-step-functions/
- https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-state-machine-structure.html
- https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html
