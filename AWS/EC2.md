# EC2 - Elastic Cloud Compute

## Auto Scaling

In Auto Scaling, the following statements are correct regarding the cooldown period:
- It ensures that the Auto Scaling group does not launch or terminate additional EC2 instances before the previous scaling activity takes effect.
- Its default value is 300 seconds.
- It is a configurable setting for your Auto Scaling group.


## AWS Compute Optimizer 

AWS Compute Optimizer recommends optimal AWS resources for your workloads to reduce costs and improve performance by using machine learning to analyze historical utilization metrics. ***AWS Compute Optimizer can give recommendations if specific instances are under-provisioned, optimal, or over-provisioned***. You must opt-in to have Compute Optimizer analyze your AWS resources. Compute Optimizer generates recommendations for the following resources:
- Amazon Elastic Compute Cloud (Amazon EC2) instances
- Amazon EC2 Auto Scaling groups
- Amazon Elastic Block Store (Amazon EBS) volumes
- AWS Lambda functions
