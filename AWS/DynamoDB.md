# DynamoDB

Amazon DynamoDB is a fast and flexible NoSQL database service for all applications that need consistent, single-digit millisecond latency at any scale. It is a fully managed cloud database and supports both document and key-value store models. Its flexible data model, reliable performance, and automatic scaling of throughput capacity makes it a great fit for mobile, web, gaming, ad tech, IoT, and many other applications.

*Since DynamoDB tables are public resources, applications within a VPC rely on an Internet Gateway to route traffic to/from Amazon DynamoDB*. You can use a **Dynamo DB Gateway endpoint** if you want to keep the traffic between your VPC and Amazon DynamoDB within the Amazon network. ***This way, resources residing in your VPC can use their private IP addresses to access DynamoDB with no exposure to the public internet***.

When you create a DynamoDB Gateway endpoint, _**you specify the VPC** where it will be deployed **as well as the route table** that will be associated with the endpoint_. The route table will be updated with an Amazon DynamoDB prefix list (list of CIDR blocks) as the destination and the endpoint’s ID as the target.

DynamoDB **on-demand backups** are available at no additional cost beyond the normal pricing that’s associated with backup storage size. DynamoDB on-demand backups cannot be copied to a different account or Region. ***To create backup copies across AWS accounts and Regions and for other advanced features, you should use AWS Backup***. With AWS Backup, you can configure backup policies and monitor activity for your AWS resources and on-premises workloads in one place. Using DynamoDB with AWS Backup, *you can copy your on-demand backups across AWS accounts and Regions*, add cost allocation tags to on-demand backups, and transition on-demand backups to cold storage for lower costs. ***To use these advanced features, you must opt into AWS Backup***. Opt-in choices apply to the specific account and AWS Region, so you might have to opt into multiple Regions using the same account.

## DynamoDB Streams

A **DynamoDB stream** is an ordered flow of information about changes to items in an Amazon DynamoDB table. When you enable a stream on a table, DynamoDB captures information about every modification to data items in the table. Whenever an application creates, updates, or deletes items in the table, DynamoDB Streams writes a **stream record** with the primary key attribute(s) of the items that were modified. A stream record contains information about a data modification to a single item in a DynamoDB table. You can configure the stream so that the stream records capture additional information, such as the “before” and “after” images of modified items.

Amazon DynamoDB is integrated with AWS Lambda so that you can create triggers—pieces of code that automatically respond to events in DynamoDB Streams. *With triggers, you can build applications that react to data modifications in DynamoDB tables*. If you enable DynamoDB Streams on a table, you can associate the stream ARN with a Lambda function that you write. Immediately after an item in the table is modified, a new record appears in the table’s stream. AWS Lambda polls the stream and invokes your Lambda function synchronously when it detects new stream records. The Lambda function can perform any actions you specify, such as sending a notification or initiating a workflow.

- DynamoDB Streams captures a time-ordered sequence of item-level modifications in any DynamoDB table and ***stores this information in a log for up to 24 hours***. Applications can access this log and view the data items as they appeared before and after they were modified, in near-real-time. 
- You can consume logs stored in DynamoDB streams in multiple ways. The most common approaches use AWS Lambda or a standalone application that uses the Kinesis Client Library (KCL) with the DynamoDB Streams Kinesis Adapter.

## *Resources*

- [Tutorials Dojo Cheat Sheet](https://tutorialsdojo.com/amazon-dynamodb/)