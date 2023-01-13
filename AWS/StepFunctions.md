# AWS Step Functions 

Step Functions is a fully managed service that makes it easy to coordinate the components of distributed applications and microservices using **visual workflows**. You define **state machines** that describe your workflow as a series of steps, their relationships, and their inputs and outputs. State machines contain a number of **states**, *each of which represents an individual step in a workflow diagram*. States can perform work, make choices, pass parameters, initiate parallel execution, manage timeouts, or terminate your workflow with a success or failure. ***With Step Functions, you write state machines in declarative JSON***. Step Functions keeps track of all tasks and events in an application. You can use Amazon SQS to build basic workflows to coordinate your distributed application, but you get this facility out-of-the-box with Step Functions, alongside other application-level capabilities.

Step Functions automatically triggers and tracks each step, and retries when there are errors so your application executes in order and as expected. With Step Functions, you can craft long-running workflows such as machine learning model training, report generation, and IT automation. You can manage the coordination of a state machine in Step Functions using the Amazon States Language. The **Amazon States Language** is a JSON-based, structured language used to define your state machine, a collection of states, that can do work (**Task states**), determine which states to transition to next (**Choice states**), stop execution with an error (**Fail states**), and so on.

## *Resources* 

- https://tutorialsdojo.com/aws-step-functions/
- https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-state-machine-structure.html
- https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html