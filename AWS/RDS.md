# RDS

_Amazon RDS provides high availability and failover support for DB instances using **Multi-AZ deployments**_. Amazon RDS uses several different technologies to provide failover support. Multi-AZ deployments for Oracle, PostgreSQL, MySQL, and MariaDB DB instances use Amazon’s failover technology. SQL Server DB instances use SQL Server Database Mirroring (DBM).

In a Multi-AZ deployment, Amazon RDS *automatically provisions and maintains a synchronous standby replica in a different Availability Zone*. The primary DB instance is **synchronously replicated** across Availability Zones to a standby replica to provide data redundancy, eliminate I/O freezes, and minimize latency spikes during system backups. The high-availability feature is not a scaling solution for read-only scenarios; *you cannot use a standby replica to serve read traffic*. To service read-only traffic, you should use a **Read Replica**.

Amazon RDS automatically performs a failover in the event of any of the following:
- Loss of availability in primary Availability Zone
- Loss of network connectivity to primary
- Compute unit failure on primary
- Storage failure on primary

In Amazon RDS, *failover is automatically handled* so that you can resume database operations as quickly as possible without administrative intervention in the event that your primary database instance goes down. When failing over, Amazon RDS *simply flips the canonical name record (CNAME) for your DB instance to point at the standby*, which is in turn **promoted to become the new primary**.

| Multi-AZ     | Read Replica   |
| ------------ | -------------- |
| Synchronous replication - highly durable | Asynchronous replication - highly scalable |
| Only DB engine on primary instance is active | All read replicas are accessible and can be used for read scaling |
| Automated backups are taken from standby | No backups configured by default |
| Always span two AZ within a single Region | Can be within AZ, Cross-AZ, or Cross-Region |
| DB engine version upgrades happen on primary | DB engine version upgrade is independent from source instance |
| Automatic failover to standby when a problem is detected | Can be manually promoted to a standalone DB instance |



## *Resources*

- [Tutorials Dojo RDS Cheat Sheet](https://tutorialsdojo.com/amazon-relational-database-service-amazon-rds/)