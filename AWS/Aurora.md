# Amazon Aurora

Amazon Aurora is a fully managed relational database engine that’s compatible with MySQL and PostgreSQL. With some workloads, Aurora can deliver up to five times the throughput of MySQL and up to three times the throughput of PostgreSQL.
- Aurora includes a high-performance storage subsystem. The underlying storage grows automatically as needed, up to 128 terabytes. The minimum storage is 10GB.
- Aurora will keep your database up-to-date with the latest patches.
- Aurora supports quick, efficient cloning operations.
   - You can share your Amazon Aurora DB clusters with other AWS accounts for quick and efficient database cloning.
- Aurora is fault-tolerant and self-healing.

Take note that a _non-Serverless DB cluster for Aurora is called a **provisioned DB cluster**_. Aurora Serverless clusters and provisioned clusters both have the same kind of high-capacity, distributed, and highly available storage volume.
- When you work with Amazon Aurora without Aurora Serverless (provisioned DB clusters), you can choose your DB instance class size and create Aurora Replicas to increase read throughput. If your workload changes, *you can modify the DB instance class size and change the number of Aurora Replicas*. This model works well when the **database workload is predictable**, because you can adjust capacity manually based on the expected workload.
- Amazon Aurora typically involves a cluster of DB instances instead of a single instance. *Each connection is handled by a specific DB instance*. When you connect to an Aurora cluster, the host name and port that you specify point to an intermediate handler called an **endpoint**. Aurora uses the endpoint mechanism to abstract these connections. Thus, you don’t have to hardcode all the hostnames or write your own logic for load-balancing and rerouting connections when some DB instances aren’t available.
- For certain Aurora tasks, *different instances or groups of instances perform different roles*. For example, the primary instance handles all data definition language (DDL) and data manipulation language (DML) statements. Up to 15 Aurora Replicas handle read-only query traffic.
- Using **endpoints**, you can map each connection to the appropriate instance or group of instances based on your use case. For example, to perform DDL statements you can connect to whichever instance is the primary instance. *To perform queries, you can connect to the reader endpoint, with Aurora automatically performing load-balancing among all the Aurora Replicas*. For clusters with DB instances of different capacities or configurations, you can connect to custom endpoints associated with different subsets of DB instances. For diagnosis or tuning, you can connect to a specific instance endpoint to examine details about a specific DB instance.
- The custom endpoint provides load-balanced database connections based on criteria other than the read-only or read-write capability of the DB instances. *For example, you might define a custom endpoint to connect to instances that use a particular AWS instance class or a particular DB parameter group*. Then you might tell particular groups of users about this custom endpoint. For example, you might direct internal users to low-capacity instances for report generation or ad hoc (one-time) querying, and direct production traffic to high-capacity instances.

## Aurora Serverless

https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless.html
Amazon Aurora Serverless is an on-demand, auto-scaling configuration for Amazon Aurora. An Aurora Serverless DB cluster is a DB cluster that automatically starts up, shuts down, and scales up or down its compute capacity based on your application’s needs. Aurora Serverless provides a relatively simple, cost-effective option for *infrequent, intermittent, sporadic or unpredictable workloads*. It can provide this because it automatically starts up, scales compute capacity to match your application’s usage and shuts down when it’s not in use.

With Aurora Serverless, *you can create a database endpoint without specifying the DB instance class size*. You set the minimum and maximum capacity. With Aurora Serverless, the database endpoint connects to a proxy fleet that routes the workload to a fleet of resources that are automatically scaled. Because of the proxy fleet, connections are continuous as Aurora Serverless scales the resources automatically based on the minimum and maximum capacity specifications. Database client applications don’t need to change to use the proxy fleet. Aurora Serverless manages the connections automatically. _Scaling is rapid because it uses a **pool of “warm” resources** that are always ready to service requests_. Storage and processing are separate, so you can scale down to zero processing and pay only for storage.

## *Resources**

- [Tutorials Dojo Cheat Sheet](https://tutorialsdojo.com/amazon-aurora/)
- [AWS Aurora Serverless docs](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless.html)