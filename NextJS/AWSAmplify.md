# Deploy Next.js to AWS Amplify

## Install and configure Amplify CLI

Install Amplify CLI globally
```
npm install -g @aws-amplify/cli
```

Configure Amplify
```
amplify configure
```
- Signs you into console and prompts you to create a new IAM user. 
    - Specify region
    - Specify username (ex. amplify-123)
- Complete the user creation in the AWS Console
    - Ensure `AdministratorAccess-Amplify` policy is checked and finish IAM user creation.
- Copy and paste the `accessKeyId` and `secretAccessKey` from the newly created IAM user into the prompts on Amplify CLI

## Set up fullstack project

### Create a new Next.js app

```
npx create-next-app next-amplified
```

### Initialize Amplify in project

Add Amplify and initialize a new project
```
amplify init
```
Follows prompts, leaving most default as Amplify infers the proper configuration based on the type of project it is being initialized in.

`amplify init` creates a top level directory called `amplify` that stores your backend definition. During the tutorial you'll add capabilities such as a GraphQL API and authentication. As you add features, the `amplify` folder will grow with infrastructure-as-code templates that define your backend stack. *Infrastructure-as-code is a best practice way to create a replicable backend stack*.

It creates a file called `aws-exports.js` in the `src` directory that holds all the configuration for the services you create with Amplify. This is how the Amplify client is able to get the necessary information about your backend services.

A cloud project is created for you in the AWS Amplify Console that can be accessed by running `amplify console`. The Console provides a list of backend environments, deep links to provisioned resources per Amplify category, status of recent deployments, and instructions on how to promote, clone, pull, and delete backend resources.

As you add or remove categories and make updates to your backend configuration using the Amplify CLI, the configuration in `aws-exports.js` will update automatically.

### Install Amplify Libraries

The first step to using Amplify in the client is to install the necessary dependencies:
```
npm install aws-amplify @aws-amplify/ui-react
```
The `aws-amplify` package is the main library for working with Amplify in your apps. The `@aws-amplify/ui-react` package includes React-specific UI components you'll use as you build the app.

## Connect API and database to the app

### Create GraphQL API and database

Add a GraphQL API to your app and automatically provision a database by running the following command from the root of your application directory:
```
amplify add api
```
- GraphQL
- Select Authorization modes: API key (default, expiration 7 days)
- Select default authorization type for API: Amazon Cognito User Pool
- Users sign in with: username
- Edit schema and replace with Post model:
    ```
    type Post
        @model
        @auth(rules: [{ allow: owner }, { allow: public, operations: [read] }]) {
        id: ID!
        title: String!
        content: String!
    }
    ```
### Deploy API

```
amplify push
```
The backend is now live

To view the GraphQL API in the AppSync console at any time, run the following command:
```
amplify console api
```

To view your entire app in the Amplify console at any time, run the following command:
```
amplify console
```
You can test your API locally with 
```
amplify mock api
```
This will open the GraphiQL explorer on a local port where you can test operations like queries and mutations. 

## API with SSR

Visit [AWS guide](https://docs.amplify.aws/start/getting-started/data-model/q/integration/next/#api-with-server-side-rendering-ssr) for detailed instructions on how to create a home page with login and list of posts, create new post, and single post pages. 

## Deploy and host Next.js app

```
amplify add hosting
```
This will open Amplify Studio in the console and allow you to select a git source repo for your app's **Frontend environments**. You will authorize your git provider and select the repo and branch for this deployment. You will need to create a new role for the deployment to use. Once connected it will provision, build, and deploy to AWS. 

## *Resources*

- https://docs.amplify.aws/start/q/integration/next/

- https://docs.amplify.aws/start/getting-started/nextsteps/q/integration/next/