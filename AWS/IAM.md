# IAM Identity Access Management

## Authorization

AWS uses values from the request context to check for policies that apply to the request. It then uses the policies to determine whether to allow or deny the request.

Policies types can be categorized as permissions policies or permissions boundaries.
- **Permissions policies** define the permissions for the object to which they’re attached. These include identity-based policies, resource-based policies, and ACLs.
- **Permissions boundary** is an advanced feature that allows you to use policies to limit the maximum permissions that a principal can have.

To provide your users with permissions to access the AWS resources in their own account, you need **identity-based policies**. In contrast, **Resource-based policies** are for granting cross-account access.

Evaluation logic rules for policies:
- *By default, all requests are denied*.
- An explicit allow in a permissions policy overrides this default.
- A permissions boundary overrides the allow. If there is a permissions boundary that applies, that boundary must allow the request. Otherwise, it is implicitly denied.
An explicit deny in any policy overrides any allows.

## Users

### IAM Users

Instead of sharing your root user credentials with others, you can create individual **IAM users** within your account that correspond to users in your organization. IAM users are not separate accounts; they are users within your account.

Each user can have its own password for access to the AWS Management Console. You can also create an individual access key for each user so that the user can make programmatic requests to work with resources in your account. By default, a brand new IAM user has NO permissions to do anything. *Users are global entities*.

### IAM Groups

- An IAM group is a collection of IAM users.
- You can organize IAM users into IAM groups and attach access control policies to a group.
- A user can belong to multiple groups.
- Groups cannot belong to other groups.
- Groups do not have security credentials, and cannot access web services directly.

### IAM Roles

A role does not have any credentials associated with it. An IAM user can assume a role to temporarily take on different permissions for a specific task. A role can be assigned to a federated user who signs in by using an external identity provider instead of IAM.

**AWS service role** is a role that a service assumes to perform actions in your account on your behalf. This service role must include all the permissions required for the service to access the AWS resources that it needs.
- **AWS service role for an EC2 instance** is a special type of service role that a service assumes to launch an EC2 instance that runs your application. This role is assigned to the EC2 instance when it is launched.
- **AWS service-linked role** is a unique type of service role that is linked directly to an AWS service. Service-linked roles are predefined by the service and include all the permissions that the service requires to call other AWS services on your behalf.

## Policies

- Most permission policies are JSON policy documents.
- The IAM console includes **policy summary tables** that describe the access level, resources, and conditions that are allowed or denied for each service in a policy.
    - The **policy summary** table includes a list of services. Choose a service there to see the **service summary**.
    - This **summary table** includes a list of the actions and associated permissions for the chosen service. You can choose an action from that table to view the action **summary**.

To assign permissions to federated users, you can create an entity referred to as a **role** and define permissions for the role.

### Identity-Based Policies

- **Permissions policies** that you attach to a principal or identity.
- **Managed policies** are standalone policies that you can attach to multiple users, groups, and roles in your AWS account.
- **Inline policies** are policies that you create and manage and that are embedded directly into a single user, group, or role.

### Resource-based Policies

- **Permissions policies** that you attach to a resource such as an Amazon S3 bucket.
- **Resource-based policies** are only inline policies.
- **Trust policies** are resource-based policies that are attached to a role and define which principals can assume the role.

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
