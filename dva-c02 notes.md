Exam Prep Website

#### A software company is launching a multimedia application. The application will allow guest users to access sample content before the users decide if they want to create an account to gain full access. The company wants to implement an authentication process that can identify users who have already created an account. The company also needs to keep track of the number of guest users who eventually create an account (Choose Two)

- **Option D** Create a role for authenticated users that allows access to all content. Create a role for unauthenticated users that allows access to only the sample content. 
- **Option B** Create an Amazon Cognito identity pool. Configure the identity pool to allow unauthenticated users. Exchange unique identity for temporary credentials that allow all users to assume a role
	**Option B because by configuring the identity pool to allow unauthenticated users, you can enable guest users to access the sample content. When users create an account, they can be authenticated, and then given access to the full content by assuming a role that allows them access**
	**Option D is correct because creating roles for authenticated and unauthenticated users with different levels of access is an appropriate wauy to meet the requirement of identifying users who have created an account and keep track of the number of guest users who eventually create an account**

#### A developer creates an AWS Lambda function that retrieves and groups data from several public API endpoints. The Lambda function has been updated and configured to connect to the private subnet of a VPC. an Internet gateway is attached to the VPC. The uses of the default network ACL and security group configurations
#### The developer finds that the Lambda function can no longer access the public API. The developer has ensure that the public API is accessible, but the Lambda function cannot connect to the API

#### How should the developer fix the connection issue?

- Ensure that the outbound traffic from the private subnet is routed to a public NAT gateway
	**When a Lambda function is configured to connect to a VPC, it loses its default internet access. To allow the Lambda function to access the public internet it must be connected to a privat subnet in the BPC that is configured to route its traffice through a NAT Gateway (Network Address Translation Gateway). 
	The Internet gateway is usually used to provide internet access to resources in the public subnet, but for resources in the private subnet, a NAT Gateway is required.**

#### A developer needs to deploy an application running on AWS Fargate using Amazon ECS. the application has environment variables that must be passed to a container for the application to initialize.
#### How should the environment variables be passed to the container?

- Define an array that includes the environment variables under the environment parameter within the task definition
	**When using ECS, the task definition is where you define parameters for your containers, including environment variables. The environment parameters within the task definition allows you to specifiy environment variables for your containers. This approach provides a clear separation of concerns, allowing you to redefine the environment variables at the task definition level, which is then used by the service when running task.**

