# Migration

## AWS Application Discovery Service 

AWS Application Discovery Service helps you plan your migration to the AWS cloud by collecting usage and configuration data about your on-premises servers. Application Discovery Service is integrated with AWS Migration Hub, which simplifies your migration tracking as it aggregates your migration status information into a single console. You can view the discovered servers, group them into applications, and then track the migration status of each application from the Migration Hub console in your home region.

Application Discovery Service gathers various server parameters such as CPU, disk, memory, and network. This collected data is encrypted in transit as well as at rest. These parameters can be discovered in any of the following two ways:
- **Agentless Discovery**: this is *suited for VMware hosts*. With this method an OVA (Open Virtual Appliance) needs to be deployed on a VM host associated with VMware vCenter. No additional software is required to discover the required parameters. This agent can collect the required information irrespective of the operating systems installed on the VMs
- **Agent-based Discovery**: suitable for collecting data for hosts other than VMware hosts. With this, agents are deployed on machines having *Windows, Linux, Ubuntu, CentOs, and SUSE operating systems*. 

## AWS Migration Hub 

AWS Migration Hub provides a single place to discover your existing servers, plan migrations, and track the status of each application migration. The Migration Hub provides visibility into your application portfolio and streamlines planning and tracking. You can ***visualize*** the connections and the status of the servers and databases that make up each of the applications you are migrating. 

Simply, AWS Migration Hub is a suite of tools such as AWS Application Migration Service, AWS Server Migration Service, AWS Database Migration Service, and ATADATA ATAmotion that are integrated with AWS Migration Hub. AWS Migration Hub can be used to track the migration activity performed by each of these tools.

## "Lift-and-shift" 

Lift-and-shift (also known as “rehost”) is a common approach for migrating to AWS, whereby you move a workload from on-premises with little or no modification. In a large legacy migration scenario where the organization is looking to scale its migration quickly to meet a business case, we find that the majority of applications are rehosted when moving to the cloud to minimize risk and speed up time to production.

## AWS Application Migration Service (MGN) 

MGN is a highly automated lift-and-shift solution that works by replicating your on-premises (physical or virtual) and/or cloud servers (referred to as “source servers”) into your AWS account. When you’re ready, ***AWS MGN automatically converts and launches your servers on AWS*** so you can quickly benefit from the cost savings, productivity, resilience, and agility of the cloud. Once your applications are running on AWS, you can leverage AWS services and capabilities to quickly and easily re-platform or refactor those applications. 

## AWS Database Migration Service (AWS DMS) 
AWS DMS is a cloud service that makes it easy to migrate relational databases, data warehouses, NoSQL databases, and other types of data stores. You can use AWS DMS to migrate your data into the AWS Cloud or between combinations of cloud and on-premises setups.

With AWS DMS, you can perform one-time migrations, and *you can replicate ongoing changes to keep sources and targets in sync*. If you want to _migrate to a different database engine, you can use the **AWS Schema Conversion Tool (AWS SCT)** to translate your database schema to the new platform_. You then use AWS DMS to migrate the data. Because AWS DMS is a part of the AWS Cloud, you get the cost efficiency, speed to market, security, and flexibility that AWS services offer.

You can use AWS DMS to migrate data to an Amazon DynamoDB table. Amazon DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability. AWS DMS supports using a relational database or MongoDB as a source.

You can migrate data to Amazon S3 using AWS DMS from any of the supported database sources. When using Amazon S3 as a target in an AWS DMS task, **both full load and change data capture (CDC) data is written to comma-separated value (.csv) format by default**. The comma-separated value (.csv) format is the default storage format for Amazon S3 target objects. For more compact storage and faster queries, you can instead use Apache Parquet (.parquet) as the storage format.

You can encrypt connections for source and target endpoints by using Secure Sockets Layer (SSL). To do so, you can use the AWS DMS Management Console or AWS DMS API to *assign a certificate to an endpoint*. You can also use the AWS DMS console to manage your certificates.


## *Resources*

- [The 6 R's](https://tutorialsdojo.com/aws-migration-strategies-the-6-rs)
- [Application Discovery Service](https://aws.amazon.com/application-discovery/faqs/)
- [AWS Migration Hub docs](https://aws.amazon.com/application-migration-service/)