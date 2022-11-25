# Simple Queue Service (SQS)

In Amazon SQS, you can configure the message retention period to a value from 1 minute to 14 days. **The default is 4 days**, max is 14 days. Once the message retention limit is reached, your messages are automatically deleted.

A single Amazon SQS message queue can contain an unlimited number of messages. However, there is a 120,000 limit for the number of inflight messages for a standard queue and 20,000 for a FIFO queue. Messages are **inflight** after they have been received from the queue by a consuming component, but have not yet been deleted from the queue.

Always remember that the messages in the SQS queue *will continue to exist* even after the EC2 instance has processed it, *until you delete that message*. You have to ensure that you delete the message after processing to prevent the message from being received and processed again once the visibility timeout expires.

See also [AWS docs SQS Basic Architecture](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-basic-architecture.html)

# Simple Notification Service (SNS)

Amazon SNS is a fully managed pub/sub messaging service. With Amazon SNS, you can use **topics** to simultaneously distribute messages to multiple subscribing endpoints such as Amazon SQS queues, AWS Lambda functions, HTTP endpoints, email addresses, and mobile devices (SMS, Push).

A **fanout scenario** occurs when a message published to an SNS topic is replicated and pushed to multiple endpoints, such as Amazon SQS queues, HTTP(S) endpoints, and Lambda functions. This allows for parallel asynchronous processing. 

By default, an Amazon SNS topic subscriber receives every message published to the topic. You can use Amazon SNS message filtering to assign a filter policy to the topic subscription, and the subscriber will only receive a message that they are interested in. *Using Amazon SNS and Amazon SQS together, messages can be delivered to applications that require immediate notification of an event*. This method is known as fanout to Amazon SQS queues.

## *Resources

- [Tutorials Dojo SQS Cheat Sheet](https://tutorialsdojo.com/amazon-sqs/)