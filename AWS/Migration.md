# Migration

## AWS Application Discovery Service 

AWS Application Discovery Service helps you plan your migration to the AWS cloud by collecting usage and configuration data about your on-premises servers. Application Discovery Service is integrated with AWS Migration Hub, which simplifies your migration tracking as it aggregates your migration status information into a single console. You can view the discovered servers, group them into applications, and then track the migration status of each application from the Migration Hub console in your home region.

Application Discovery Service gathers various server parameters such as CPU, disk, memory, and network. This collected data is encrypted in transit as well as at rest. These parameters can be discovered in any of the following two ways:
- **Agentless Discovery**: this is *suited for VMware hosts*. With this method an OVA (Open Virtual Appliance) needs to be deployed on a VM host associated with VMware vCenter. No additional software is required to discover the required parameters. This agent can collect the required information irrespective of the operating systems installed on the VMs
- **Agent-based Discovery**: suitable for collecting data for hosts other than VMware hosts. With this, agents are deployed on machines having *Windows, Linux, Ubuntu, CentOs, and SUSE operating systems*. 

## AWS Migration Hub 

AWS Migration Hub provides a single place to discover your existing servers, plan migrations, and track the status of each application migration. The Migration Hub provides visibility into your application portfolio and streamlines planning and tracking. You can ***visualize*** the connections and the status of the servers and databases that make up each of the applications you are migrating.

## "Lift-and-shift" 

Lift-and-shift (also known as “rehost”) is a common approach for migrating to AWS, whereby you move a workload from on-premises with little or no modification. In a large legacy migration scenario where the organization is looking to scale its migration quickly to meet a business case, we find that the majority of applications are rehosted when moving to the cloud to minimize risk and speed up time to production.

## AWS Application Migration Service (MGN) 

MGN is a highly automated lift-and-shift solution that works by replicating your on-premises (physical or virtual) and/or cloud servers (referred to as “source servers”) into your AWS account. When you’re ready, ***AWS MGN automatically converts and launches your servers on AWS*** so you can quickly benefit from the cost savings, productivity, resilience, and agility of the cloud. Once your applications are running on AWS, you can leverage AWS services and capabilities to quickly and easily re-platform or refactor those applications.

## *Resources*

- [The 6 R's](https://tutorialsdojo.com/aws-migration-strategies-the-6-rs)
- [Application Discovery Service](https://aws.amazon.com/application-discovery/faqs/)