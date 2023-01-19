# DynamoDB

Amazon DynamoDB is a fast and flexible NoSQL database service for all applications that need consistent, single-digit millisecond latency at any scale. It is a fully managed cloud database and supports both document and key-value store models. Its flexible data model, reliable performance, and automatic scaling of throughput capacity makes it a great fit for mobile, web, gaming, ad tech, IoT, and many other applications.

The **partition key** portion of a table’s primary key determines the logical partitions in which a table’s data is stored. This in turn affects the underlying physical partitions. Provisioned I/O capacity for the table is divided evenly among these physical partitions. Therefore a partition key design that doesn’t distribute I/O requests evenly can create *“hot” partitions that result in throttling and use your provisioned I/O capacity inefficiently*.

***The optimal usage of a table’s provisioned throughput depends not only on the workload patterns of individual items, but also on the partition-key design***. This doesn’t mean that you must access all partition key values to achieve an efficient throughput level, or even that the percentage of accessed partition key values must be high. It does mean that the more distinct partition key values that your workload accesses, the more those requests will be spread across the partitioned space. ***In general, you will use your provisioned throughput more efficiently as the ratio of partition key values accessed to the total number of partition key values increases***. One example for this is the use of partition keys with **high-cardinality attributes, which have a large number of distinct values for each item**. [^1]

For DynamoDB, it scales well due to these reasons:
- Its schema flexibility lets DynamoDB store complex hierarchical data within a single item. DynamoDB is not a totally schemaless database since the very definition of a schema is just the model or structure of your data.
- Composite key design lets it store related items close together on the same table.

*Since DynamoDB tables are public resources, applications within a VPC rely on an Internet Gateway to route traffic to/from Amazon DynamoDB*. You can use a **Dynamo DB Gateway endpoint** if you want to keep the traffic between your VPC and Amazon DynamoDB within the Amazon network. ***This way, resources residing in your VPC can use their private IP addresses to access DynamoDB with no exposure to the public internet***.

When you create a DynamoDB Gateway endpoint, _**you specify the VPC** where it will be deployed **as well as the route table** that will be associated with the endpoint_. The route table will be updated with an Amazon DynamoDB prefix list (list of CIDR blocks) as the destination and the endpoint’s ID as the target.

DynamoDB **on-demand backups** are available at no additional cost beyond the normal pricing that’s associated with backup storage size. DynamoDB on-demand backups cannot be copied to a different account or Region. ***To create backup copies across AWS accounts and Regions and for other advanced features, you should use AWS Backup***. With AWS Backup, you can configure backup policies and monitor activity for your AWS resources and on-premises workloads in one place. Using DynamoDB with AWS Backup, *you can copy your on-demand backups across AWS accounts and Regions*, add cost allocation tags to on-demand backups, and transition on-demand backups to cold storage for lower costs. ***To use these advanced features, you must opt into AWS Backup***. Opt-in choices apply to the specific account and AWS Region, so you might have to opt into multiple Regions using the same account.

## API Retries

When your program sends a request, DynamoDB attempts to process it. If the request is successful, DynamoDB returns an HTTP success status code (`200 OK`), along with the results from the requested operation. If the request is unsuccessful, DynamoDB returns an error.

An HTTP `400` status code indicates a problem with your request, such as authentication failure, missing required parameters, or exceeding a table’s provisioned throughput. You have to fix the issue in your application before submitting the request again.

`ProvisionedThroughputExceededException` means that your request rate is too high. The AWS SDKs for DynamoDB automatically retries requests that receive this exception. Your request is eventually successful unless your retry queue is too large to finish. To handle this error, you can reduce the frequency of requests using error retries and exponential backoff.

## DynamoDB Streams

A **DynamoDB stream** is an ordered flow of information about changes to items in an Amazon DynamoDB table. When you enable a stream on a table, DynamoDB captures information about every modification to data items in the table. Whenever an application creates, updates, or deletes items in the table, DynamoDB Streams writes a **stream record** with the primary key attribute(s) of the items that were modified. A stream record contains information about a data modification to a single item in a DynamoDB table. You can configure the stream so that the stream records capture additional information, such as the “before” and “after” images of modified items.

Amazon DynamoDB is integrated with AWS Lambda so that you can create triggers—pieces of code that automatically respond to events in DynamoDB Streams. *With triggers, you can build applications that react to data modifications in DynamoDB tables*. If you enable DynamoDB Streams on a table, you can associate the stream ARN with a Lambda function that you write. Immediately after an item in the table is modified, a new record appears in the table’s stream. AWS Lambda polls the stream and invokes your Lambda function synchronously when it detects new stream records. The Lambda function can perform any actions you specify, such as sending a notification or initiating a workflow.

- DynamoDB Streams captures a time-ordered sequence of item-level modifications in any DynamoDB table and ***stores this information in a log for up to 24 hours***. Applications can access this log and view the data items as they appeared before and after they were modified, in near-real-time. 
- You can consume logs stored in DynamoDB streams in multiple ways. The most common approaches use AWS Lambda or a standalone application that uses the Kinesis Client Library (KCL) with the DynamoDB Streams Kinesis Adapter.

## *Resources*

- [Tutorials Dojo Cheat Sheet](https://tutorialsdojo.com/amazon-dynamodb/)
[^1]: [Partition key AWS docs](https://aws.amazon.com/blogs/database/choosing-the-right-dynamodb-partition-key/)
- [AWS docs API retries](https://docs.aws.amazon.com/general/latest/gr/api-retries.html)