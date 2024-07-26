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

#### A company uses AWS Lambda functions and an Amazon S3 trigger to process images into an S3 bucket. A development team set up multiple environments in a single AWS account.
#### After a recent production deployment, the development team observed that the deployment S3 bucket invoked the production environment Lambda functions. these invocations caused unwanted execution of development S3 files by using production Lambda fucntions. The development team must prevent these invocations. The team must follow security best practices.

- Move the development and production environments into separate AWS accounts. Add a resource policy to each lambda function to allow only S3 buckets that are within the same account to invoke the function.
	**It says that the team should follow the best security practices. AWS well architectured framework suggest separation. This follows best practices**

#### A company is building as serverless application on AWS. The application uses an AWS lambda function to process customer orders 24 hours a day, 7 days a week. The Lambda function calls an external vendor's HTTP API to process payments.
#### During load tests, a developer discovers that the external vendor payment processing API occasionally times out and returns errors. The company expects that some payment processing APU calls will return errors
#### The company wants the support team to recieve notifications in near real time only when the payment processing external API error rate exceeds 5% of the total number of transactions in an hour. Developers need to use an existing Amazon Simple Notification Service (Amazon SNS) topic that is configured to notify the support team.

- Publish custom metrics to CloudWatch that record the failures of the external payment processing API calls. Configure a CloudWatch alarm to notify the existing SNS topic when error rate exceeds the specified rate.
	**With CloudWatch custom metrics, developers can publish and monitor custom data points, including the number of failed request to the external payment processing API. A CloudWatch alarm can be configured to notify an SNS topic when the error rate exceeds the specified rate, allowing the support team to be notified in near real-time.**

#### A company is implementing an application on Amazon EC2 instances. The applicationm needs to process incoming transactions. when the application detects a transaction that is not valid, the application must send a chat message to the company's support team. To send the message, the application needs to retrieve the access token to authenticate by using the chat API
#### A developer needs to implement a solution to store the access token. The access token must be encrypted at rest and in transit. The access token must also be accessible from other AWS accounts. (LEAST management overhead)

- Use Secrets Manager with an AWS key Mangement Service  customer managed key to store the access token. Add a resource-based policy to the secret to allow access from other accounts. Update the IAM role of the EC2 instances with permissions to access Secrets Manager. Retrieve the token from Secrets Manager. Use the decrypted access token to send the message to the chat.
	**Since the question says the LEAST management overhead. The answer cannot be any other because they suggest to use a customer managed key**

#### A developer built an application that calls an external API to obtain data, processes the data, and saves the result to Amazon S3. The developer built a container image with all of the necessary dependencies to run the application as a container
#### The application runs locally and requires minimal CPU and RAM resources. The developer has created an Amazon ECS cluster, The developer needs to run the application hourly in Amazon Elastic Container Service (Amazon ECS) (LEAST amount of infrastructure management overhead)

- Define a task definition with an AWS Fargate launch type.
	**Usually with ECS with Fargate is the least management**

#### A developer is building an application on AWS. The applucation includes an AWS Lambda function that processes the messages from an Amazon Simple Queue Service (Amazon SQS) queue.
#### The Lambda function sometimes fails or times out. The developer needs to figure out why the Lambda function fails to process some messages (LEAST operational overhead)

- Create a dead-letter queue. Configure the Lambda function to send the failed messages to the dead-letter queue.
	**Always Dead letter queue for checking failed processed messaged in Lambda**

#### A developer is incorporating AWS X-ray into an application that handles personal identifiable information (PII). The application is hosted on Amazon EC2 instances. The application trace messages include encrypted PII and go to Amazon CloudWatch. The developer needs to ensure that no PII goes outside of the EC2 Instances.

- Manually instrument the X-Ray SDK in the application code
	**By manually instrumenting the X-Ray SDK in the application code, the developer can have full control over which data is included in the trace messages. This way, the developer can ensure that no PII is sent to X-Ray by carefully handling the PII within the application and not including it in the trace messages.** Christian said whenever you see trace or distribute that you should think X-ray

#### A developer is creating an AWS CloudFormation template to deploy Amazon EC2 Instances across multiple AWS accounts. The developer must choose the EC2 instance from a list of approved instance types.
#### how can the developer incorporate the list of approved instance types in the CloudFormation template. 

- In the CloudFormation template, create a parameter with the list of EC2 instance types as AllowedValues
	**In the CloudFormation template, the developer should create a parameter with the list of approved EC2 instance types as AllowedValues. THis way, users can select the instance type they wan to use when launching the CloudFormation stack, but only from the approved list.**

#### A developer registered a AWS Lambda function as a target for an Application Load Balancer (ALB) using a CLI command. However, the Lambda function is not being invoked when the client sends request through the ALB.
#### Why is the Lambda function not being invoked?

- The permissions to invoke the Lambda function are missing
	**To allow an ALB to invoke a Lambda function, you need to grant the ALB permission to invoke the Lambda. This is typically done by adding a resource-based policy to the Lambda function, granting invoke permission to the ALB. If this permission is not set, the ALB will not be able to trigger the Lambda function in response to incoming request.**

#### A company is releasing a new feature. Users can request early access to the new feature by using an application form. The company expects a surge of request when the application becomes available. Each request will be stored as an item in an Amazon DynamoDB table. 
#### Each item will contain the user's username, the submission date, and a validation status of UNVALIDATED. VALID, or NOT VALID. Each item also will contain the user's rating of the process on a scale of 1 to 5.
#### Each user can submit one request. For the DynamoDB table, the developer must choose a partition key that will give the workload well-distributed records across partitions.
#### Which DynamoDB attribute will meet these requirements?

- Username
	**Username avoids a hot partition key**

#### A development team maintains a web application by using a single AWS CloudFormation template. The template defines web servers and an Amazon RDS database. The team uses the Cloud Formation template to deploy the Cloud Formation Stack to different environments.
#### During a recent application deployment, a developer caused the primary development database to be dropped and recreated. The result of this incident was a loss of data. The team needs to avoid accidental database deletion in the future.

- (**Option B**) Update the CloudFormation stack policy to prevent updates to the database
- (**Option A**) Add a CloudFormation Deletion Policy attribute with the Retain value to the database resource
	**Option A, Add a CloudFormation Deletion Policy attribute with the retain to the database resource: By adding a Deletion Policy attribute with the Retain value to the database resource in the CloudFormation template, the database will not be deleted even if the Cloud Formation stack is deleted. This helps prevent accidental database loss during stack deletion**
	**Update the CloudFormation stack policy to prevent updates to the database: By updating the CloudFormation stack policy, the development team can restrict updates to the database resource. This prevents accidental modifications or recreations of the database during stack updates. The stack policy can define specific actions that are allowed or denied, providing an additional layer of protection against unintentional database changes**

#### A Company is using Amazon API Gateway to invoke a new AWS Lambda function versions in its PROD and DEV environments. In each environment, there is a Lambda function alias pointing to the corresponding Lambda function version. API Gateway has one stage that is configured to point at the PROD alias.
#### The company wants to configure API Gateway to enable the PROD and DEV Lambda function versions to be simultaneously and distinctly available.

- Use an API Gateway stage variable to configure the Lambda function alias. Republish PROD and create a new stage for development. Create API Gateway stage variables for PROD and DEV stages. Point each stage variable to the PROD Lambda function alias and to the DEV Lambda function alias.
	**Use an API Gateway stage variable to configure the Lambda function alias**

#### Users are reporting errors in an application. The application consist of several microservices that are deployed on Amazon Elastic Container Service (Amazon ECS) with AWS Fargate
#### Which combination of steps should a developer take to fix the errors? (Choose Two.)

A Daemon is **a type of computer program that runs in the background, performing various tasks without direct interaction from the user**

- (**Option A**) Deploy AWS X-Ray as a sidecar container to the microservices. update the task role policy to allow access to the X-Ray API
- (**Option D**) Instrument the application by using the AWS X-Ray SDK. Update the application to communicate with the X-Ray daemon.
	**Option A: X-Ray Container as a "Side Car" in ECS/Fargate cluster**
	**Option D: Instrument the application using the AWS X-Ray SDK to collect telemetry data** 

#### An ecommerce application is running behind an Application Load Balancer. A developer observes some unexpected load on the application during non-peak hours. The developer wants to analyze patterns for the client IP addresses that use the application
#### Which HTTP header should the developer use for this analysis

- The X-Forwarded-For header
	**original IP address of a client**
	
	HTTP Headers
	**X-Forwarded-For is a standard request header that identifies the IP address of a client when it connect s to a we server through proxy server**
	X-Forwarded Proto: protocol (HTTP/HTTPS)
	X-Forwarded Host: original Host header requested by the client
	X-Forwarded For: original IP address of a client
	X-Forwarded Port: original port that the client used to connect

#### A company stores its data in data tables in a series of Amazon S3 buckets. The company received an alert that customer credit card information might have been exposed in a data table on one of the company's public applications. A developer needs to identify all potential exposures within the application environment.

- Use Amazon Macie to run a job on S3 buckets that contain the affected data. Filter the findings by using the SensitiveData:S3Object/Financial finding type
	**Amazon macie is a security service that uses machine learning and pattern matching to discover and protect sensitive data in AWS. Macie is designed to identify various types of sensitive data, including financial data, which would cover credit card information. This option is suitable for the requirement as it leverages Macie's capability to specifically identify and report on exposures of sensitive financial data**

#### A company built a new application in the AWS Cloud. The company automated the bootstrapping of new resources with an Auto Scaling group by using AWS CloudFormation templates. The bootstrap scripts contain sensitive data
#### The company needs a solution that is integrated with CloudFormation to manage the sensitive data in the bootstrap scripts
#### Which solution will meet these requirements in the MOST Secure way?

- Put the sensitive data into AWS Systems Manager Parameter Store as a secure string parameter. Update the CloudFormation templates to use dynamic references to specify template values
	**ITs the most secure solution: Sensitive data is stored in AWS Systems Manager Parameter Store, which is a secret managment service managed by AWS. Secure string parameters in AWS Systems Manager Parameter Store are encrypted with an AWS KMS key
	It's integrated with CloudFormation: Secure String parameters can be referenced in CloudFormation templates using dynamic references. This means that sensitive data does not need to be stored in CloudFormation code. **

#### A developer is building a serverless application that runs on AWS. The developer wants to create an accelerated development workflow that deploys incremental changes to AWS for testing. The developer wants to deploy the incremental changes but does not want to fully deploy the entire application to AWS for every code commit.
#### What should the developer do to meet these requirements?

- Use the AWS Serverless Application Model (AWS SAM) to build the application. Use the sam sync command to deploy the incremental changes
	**CDK synth command is not used for deploying changes. Instead, CDK synth generates an AWS CloudFormation template from the CDK app's code, which describes the cloud resources that need to be created or updated. It does not actually deploy those changes to AWS**
	
	**SAM Init: is used to initialize a new serverless application**
	**CDK Bootstrap: the main purpose of CDK bootstrap is to provision a set of resources required to support the deployment of AWS CDK applications**
	**CDK Synth: only constructs your CloudFormation template. It does not deploy (create actual resources) it to AWS. You can take the template constructed, deploy it manually in CFN console, edit or inspect**

#### A company is building a compute-intensive application that will run on a fleet of Amazon EC2 instances. The application uses attached Amazon Elastic Block Store (Amazon EBS) volumes for storing data. The Amazon EBS volumes will be created at time of initial deployment. The application will process sensitive information. All of the data must be encrypted. The solution should not impact the application's performance

- Configure the fleet of EC2 Instances to sue encrypted EBS volumes to store data.
	**This approach directly meets the requirement for encryption without impacting performance significantly. AWS EBS encryption offers encryption at rest and integrates with AWS KMS for managing encryption keys. This encryption happens transparently. to the applications using the EBS volumes, thus not affecting performance in a manner that would be significant for most compute-intensive applications. **

#### A company needs to deploy all its cloud resopurces by using AWS CloudFormation templates. A developer must create an AWS SNS automatic notification to help enforce this rule. The developer creates an SNS topic and subscribes the email address of the company's security team to the SNS topic.
#### The security team must receive a notification immediately if an IAM role is created without the use of CloudFormation

- Create an Amazon EventBridge rule to filter events from CloudTrail if a role was created without CloudFormation. Specify the SNS topic as the target of the EventBridge rule.

#### A developer is creating a serverless application that uses an AWS Lambda function. The developer will use AWS CloudFormation to deploy the application. The application will write logs to Amazon CloudWatch logs. the developer has created a log group in a CloudFormation template for the application to use. The developer needs to modify the CloudFormation template to make the name of the log group available to the application at runtime. 

- Pass the log group's Amazon Resource Name (ARN) as an environment variable to the Lambda function
	**By specifying the log group's ARN as an environment variable ion the Cloud Formation template for the Lambda function, the developer can easily access this information within the application code at runtime. The method provides a straightforward way to pass dynamic configuration or resource references to AWS Lambda functions without hardcoding values, thereby maintaining flexibility and ensuring that the application can utilize the correct resources after the deployment.**

#### A company has a multi-node windows legacy application that runs on premises. The application uses a network shared folder as a centralized configuration repository to store configuration files in .xml format. The company is migrating the application to Amazon Ec2 instances. As part of the migration to AWS, a developer must identify a solution that provides high availability for the repository.

- Create an Amazon S3 Bucket to hiost the repository. Migrate the existing .xml files to the S3 bucket. Update the application code to use the AWS SDK to read and write configuration files from Amazon S3
	**The most cost effective solution to provide high availability for the centralized configuration repository. Amazon S3 provides a highly durable and available object storage service. S3 stores objects redundantly across multiple devices and multiple facilities within a region, making it highly available. The developer can migrate the existing .xml files to an S3 bucket and update the application code to use the AWS SDK to read and write configuration files from Amazon S3**

#### An organization is storing large files in Amazon S3, and is writing a web application to display meta-data about the files to end-users. Based on the metadata a user selects an object to download. The organization needs a mechanism to index the files and provide single-digit millisecond latency retrieval for the metadata. 
#### What AWS Service should be used to accomplish this?
- Amazon DynamoDB
	**In this scenario, the metadata about the files can be stored in a DynamoDB table with a primary key based on the metadata attributes. This would enable the organization quickly query and retrieve metadata about the files in real-time, with single-digit millisecond latency** 

#### A company has an application that uses Amazon Cognito user pools as an identity provider. The company must secure access to user records. The company has set up multi-factor authentication (MFA). The company also wants to send a login activity notification by email every time a user logs in. 
#### What is the MOST operationally effiecient solution that meets this requirement?
- Configure Amazon Cognito to stream all logs to Amazon Kinesis Data Firehose. Create an AWS Lambda function to process the streamed logs and to send the email notification based on the login status 