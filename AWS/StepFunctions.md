# AWS Step Functions 

Step Functions is a fully managed service that makes it easy to coordinate the components of distributed applications and microservices using **visual workflows**. You define **state machines** that describe your workflow as a series of steps, their relationships, and their inputs and outputs. State machines contain a number of **states**, *each of which represents an individual step in a workflow diagram*. States can perform work, make choices, pass parameters, initiate parallel execution, manage timeouts, or terminate your workflow with a success or failure. ***With Step Functions, you write state machines in declarative JSON***. Step Functions keeps track of all tasks and events in an application. You can use Amazon SQS to build basic workflows to coordinate your distributed application, but you get this facility out-of-the-box with Step Functions, alongside other application-level capabilities.

Step Functions automatically triggers and tracks each step, and retries when there are errors so your application executes in order and as expected. With Step Functions, you can craft long-running workflows such as machine learning model training, report generation, and IT automation. You can manage the coordination of a state machine in Step Functions using the Amazon States Language. The [Amazon States Language](#amazon-states-language) is a JSON-based, structured language used to define your state machine, a collection of states, that can do work (**Task states**), determine which states to transition to next (**Choice states**), stop execution with an error (**Fail states**), and so on.

## Amazon States Language

A Step Functions execution receives a JSON text as input and passes that input to the first state in the workflow. Individual states receive JSON as input and usually pass JSON as output to the next state. Understanding how this information flows from state to state and learning how to filter and manipulate this data is key to effectively designing and implementing workflows in AWS Step Functions.

In the Amazon States Language, these fields filter and control the flow of JSON from state to state:
- `InputPath`
- `OutputPath`
- `ResultPath`
- `Parameters`

Both the `InputPath` and `Parameters` fields provide a way to manipulate JSON as it moves through your workflow. `InputPath` can limit the input that is passed by filtering the JSON notation by using a path. The `Parameters` field enables you to pass a collection of *key-value pairs*, where the values are either static values that you define in your state machine definition, or that are selected from the input using a path.

AWS Step Functions applies the `InputPath` field first, and then the `Parameters` field. You can first filter your raw input to a selection you want using `InputPath`, and then apply `Parameters` to manipulate that input further, or add new values.

The output of a state can be a copy of its input, the result it produces (for example, the output from a Task state’s Lambda function), or a combination of its input and result. Use `ResultPath` to control which combination of these is passed to the state output.

`OutputPath` enables you to select a portion of the state output to pass to the next state. This enables you to filter out unwanted information, and pass only the portion of JSON that you care about.

## *Resources* 

- https://tutorialsdojo.com/aws-step-functions/
- https://docs.aws.amazon.com/step-functions/latest/dg/amazon-states-language-state-machine-structure.html
- https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html
- https://docs.aws.amazon.com/step-functions/latest/dg/concepts-input-output-filtering.html
- https://docs.aws.amazon.com/step-functions/latest/dg/how-step-functions-works.html