# ECS
 
**Amazon Elastic Container Service (ECS)** allows you to run Docker-based containers on the cloud. Amazon ECS has two launch types for operation: EC2 and Fargate. The EC2 launch type provides EC2 instances as hosts for your Docker containers. For the Fargate launch type, AWS manages the underlying hosts so you can focus on managing your containers instead. The details and configuration on how you want to run your containers are defined on the **ECS Task Definition** which includes options on networking mode. 

Docker containers are particularly suited for batch job workloads. Batch jobs are often short-lived and embarrassingly parallel. You can package your batch processing application into a Docker image so that you can deploy it anywhere, such as in an Amazon ECS task.

Amazon ECS supports batch jobs. You can use Amazon ECS Run Task action to run one or more tasks once. The Run Task action starts the ECS task on an instance that meets the task’s requirements including CPU, memory, and ports.

*You have to create an IAM Role that the ECS task assumes in order to get access to the S3 buckets and SQS queue*. Note that the permissions of the IAM role don’t specify the S3 bucket ARN for the incoming bucket. This is to avoid a circular dependency issue in the CloudFormation template. You should always make sure to assign the least amount of privileges needed to an IAM role.

You can use Amazon EventBridge to run Amazon ECS tasks when certain AWS events occur. You can set up an EventBridge rule that runs an Amazon ECS task whenever a file is uploaded to a certain Amazon S3 bucket using the Amazon S3 PUT operation.

Amazon ECS enables you to inject sensitive data into your containers by storing your sensitive data in either **AWS Secrets Manager secrets** or **AWS Systems Manager Parameter Store parameters** and then referencing them in your container definition. The parameter that you reference can be from a different Region than the container using it, but must be from within the same account. This feature is supported by tasks using both the EC2 and Fargate launch types.

## ECR

Amazon Elastic Container Registry (ECR) is a managed AWS Docker registry service. ECR supports Docker Registry HTTP API V2 allowing you to use Docker CLI commands or your preferred Docker tools in maintaining your existing development workflow. *ECR stores your container images in Amazon S3.*

# EKS

**Amazon Elastic Kubernetes Service (EKS)** provisions and scales the Kubernetes control plane, including the API servers and backend persistence layer, *across multiple AWS availability zones for high availability* and fault tolerance. Amazon EKS automatically detects and replaces unhealthy control plane nodes and provides patching for the control plane. Amazon EKS is integrated with many AWS services to provide scalability and security for your applications. These services include Elastic Load Balancing for load distribution, IAM for authentication, Amazon VPC for isolation, and AWS CloudTrail for logging .Kubernetes is considered cloud-agnostic because it allows you to move your containers to other cloud service providers.


## *Resources*

- [Tutorials Dojo ECS Cheat Sheet](https://tutorialsdojo.com/amazon-elastic-container-service-amazon-ecs/)

- [Tutorials Dojo ECR Cheat Sheet](https://tutorialsdojo.com/amazon-elastic-container-registry-amazon-ecr/)

- [Tutorials Dojo EKS Cheat Sheet](https://tutorialsdojo.com/amazon-elastic-kubernetes-service-eks/)