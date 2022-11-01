# IAM Identity Access Management

## Initial set up of IAM user and groups

When you first create an AWS account you create an account as a **root user**. But as a best practice *do not use the AWS account root user for any task where it's not required*. Instead, create a new IAM user for each person that requires administrator access. Then make those users administrators by placing the users into an "Administrators" user group to which you attach the `AdministratorAccess` managed policy.

Thereafter, the users in the administrators user group should set up the user groups, users, and so on, for the AWS account. All future interaction should be through the AWS account's users and their own keys instead of the root user. However, to perform some account and service management tasks, you must log in using the root user credentials.

The steps in general are:
- In IAM add user with username `Administrator`
- Give AWS Management Console access
- Add user to group and create that group as `Administrators`
- Select the `AdministratorAccess` policy for that group

After you create an IAM user log out of the root user and log in via the sign-in link or with the 12 digit account ID. Sign in link will be in this format: `https://012345678912.signin.aws.amazon.com/console`. Follow instructions provided by AWS: [Creating first IAM admin user/group AWS docs](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html)

## Roles

Always remember that you should associate IAM roles to EC2 instances and not an IAM user, for the purpose of accessing other AWS services. IAM roles are designed so that your applications can securely make API requests from your instances, without requiring you to manage the security credentials that the applications use. Instead of creating and distributing your AWS credentials, you can delegate permission to make API requests using IAM roles.

The best practice in handling API Credentials is to create a new role in the Identity Access Management (IAM) service and then assign it to a specific EC2 instance. In this way, you have a secure and centralized way of storing and managing your credentials. Instead of creating and distributing your AWS credentials, you can delegate permission to make API requests using IAM roles as follows:
1. Create an IAM role.
2. Define which accounts or AWS services can assume the role.
3. Define which API actions and resources the application can use after assuming the role.
4. Specify the role when you launch your instance, or attach the role to an existing instance.
5. Have the application retrieve a set of temporary credentials and use them.

Source: [IAM roles for EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-roles-for-amazon-ec2.html)



## *Resources*

- [Creating first IAM admin user/group AWS docs](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html)
- [IAM roles for EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-roles-for-amazon-ec2.html)
- [Tutorials Dojo IAM Cheat Sheet](https://tutorialsdojo.com/aws-identity-and-access-management-iam/)
