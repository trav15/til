- [SQS](#simple-queue-service-sqs)
- [SNS](#simple-notification-service-sns)
- [Amazon MQ](#amazon-mq)
- [SWF](#amazon-simple-workflow-swf)

# Simple Queue Service (SQS)

In Amazon SQS, you can configure the message retention period to a value from 1 minute to 14 days. **The default is 4 days**, max is 14 days. Once the message retention limit is reached, your messages are automatically deleted.

A single Amazon SQS message queue can contain an unlimited number of messages. However, there is a 120,000 limit for the number of inflight messages for a standard queue and 20,000 for a FIFO queue. Messages are **inflight** after they have been received from the queue by a consuming component, but have not yet been deleted from the queue.

Always remember that the messages in the SQS queue *will continue to exist* even after the EC2 instance has processed it, *until you delete that message*. You have to ensure that you delete the message after processing to prevent the message from being received and processed again once the visibility timeout expires.

See also [AWS docs SQS Basic Architecture](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-basic-architecture.html)

# Simple Notification Service (SNS)

Amazon SNS is a fully managed pub/sub messaging service. With Amazon SNS, you can use **topics** to simultaneously distribute messages to multiple subscribing endpoints such as Amazon SQS queues, AWS Lambda functions, HTTP endpoints, email addresses, and mobile devices (SMS, Push).

A **fanout scenario** occurs when a message published to an SNS topic is replicated and pushed to multiple endpoints, such as Amazon SQS queues, HTTP(S) endpoints, and Lambda functions. This allows for parallel asynchronous processing. 

By default, an Amazon SNS topic subscriber receives every message published to the topic. You can use Amazon SNS message filtering to assign a filter policy to the topic subscription, and the subscriber will only receive a message that they are interested in. *Using Amazon SNS and Amazon SQS together, messages can be delivered to applications that require immediate notification of an event*. This method is known as fanout to Amazon SQS queues.

# Amazon MQ

Amazon MQ is a **managed message broker service** that makes it easy to migrate to a message broker in the cloud. A message broker allows software applications and components to communicate using various programming languages, operating systems, and formal messaging protocols. Amazon MQ supports Apache ActiveMQ, RabbitMQ, and other message broker engine types.

A **cluster deployment** is a logical grouping of three RabbitMQ broker nodes behind a Network Load Balancer, each sharing users, queues, and a distributed state across multiple Availability Zones (AZ). In a cluster deployment, Amazon MQ automatically manages broker policies to enable classic mirroring across all nodes, ensuring high availability (HA). Each mirrored queue consists of one main node and one or more mirrors. Each queue has its own main node. All operations for a given queue are first applied on the queue’s main node and then propagated to mirrors. Amazon MQ creates a default system policy that sets the ha-mode to all and ha-sync-mode to automatic. This ensures that data is replicated to all nodes in the cluster across different Availability Zones for better durability.

The default policy should not be deleted. If you do delete this policy, Amazon MQ will automatically recreate it. Amazon MQ will also ensure that HA properties are applied to all other policies that you create on a clustered broker. If you add a policy without the HA properties, Amazon MQ will add them for you. If you add a policy with different high-availability properties, Amazon MQ will replace them.

# Amazon Simple Workflow (SWF)

Amazon SWF provides useful guarantees around task assignments. ***It ensures that a task is never duplicated and is assigned only once***. Thus, even though you may have multiple workers for a particular activity type (or a number of instances of a decider), Amazon SWF will give a specific task to only one worker (or one decider instance). Additionally, Amazon SWF keeps at most one decision task outstanding at a time for workflow execution. Thus, you can run multiple decider instances without worrying about two instances operating on the same execution simultaneously. *These facilities enable you to coordinate your workflow without worrying about duplicate, lost, or conflicting tasks*.

## *Resources

- [Tutorials Dojo SQS Cheat Sheet](https://tutorialsdojo.com/amazon-sqs/)
- [Tutorials Dojo Amazon MQ Cheat Sheet](https://tutorialsdojo.com/amazon-mq/)
- [Tutorials Dojo SWF Cheat Sheet](https://tutorialsdojo.com/amazon-simple-workflow-amazon-swf/)