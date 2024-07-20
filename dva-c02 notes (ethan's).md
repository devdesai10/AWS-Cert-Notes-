#### The "Code" Tools
- **AWS CodePipeline** automates CI/CD (Continuous Integration/ Continuous Delivery) workflows 
	- use stages to add new sections to deployments, such as an approval stage to approve the source code for production deployment by a project owner (kinda like a PR request in GitHub)
- **AWS CodeCommit** is used for version control
- **AWS CodeDeploy** deploys code lol
	- has an optional predefined canary deployment configuration
		- canary deployments are useful when we want to limit the exposure of potential bugs/errors to consumers. 
		- canary is done by gradually exposing the new deployment.
- **AWS CommitVisualizer** is literally just to visualize commits like normal.
- **AWS X-Ray** is the best tool for analyzing performance issues in distributed applications. X-Ray provides an overview of the call stack (including Lambda functions and other components).
	- **Key Scenario**: Analyze/Investigate performance issues in distributed applications
- **AWS Step Function** is used to build distributed applications, automate processes, orchestrate microservices, and create data and machine learning (ML) pipelines
	- **Keywords:**
		- State Machine
- The easiest way to resolve merge conflicts with the least development effort is to *stop the pull from the main branch to the feature branch and rebase the feature branch from the main branch*.
- Use CodePipeline alongside CodeBuild to invoke builds and deployments when configured source controlled branches have PRs merged.
	- **Key Scenario**: If several devs are committing code to an app that uses source control

#### Common Functions/Methods
- **aws:SecureTransport**: encryption in transit, condition is boolean (true or false)
- **iam:AssumeRole**: assigns permission/policies
- **ec2:DescribeInstances**: describe ec2 instances
- **sam sync**: automatically observes local code changes and synchronizes them to AWS without building and deploying every function in the project
- you can query metadata (such as an IPV4 address) using **169.254.169.254/latest/meta-data**
- *Random Ass Functions:*
	- **sam init**: initializes a new serverless app
	- **cdk synth**: constructs CloudFormation template, DOES NOT DEPLOY
	- **cdk bootstrap**: provision a set of resources required to support the deployment of AWS CDK apps


#### CloudWatch + CloudTrail
- You can provide near real-time alerts based on custom metrics (such as API calls) by using SNS and CloudWatch custom metrics to record external API calls alongside CloudWatch alarm for notifying the states of the specific call when a rate limit is met.
	- **Key Scenario:** an app requires real-time alert based on some ambiguous invocation
- You can create an IAM policy based on all the actions CloudTrail recorded for the IAM role in a specific time frame
- How to add permissions to a Lambda action. 
	- example to implement `ec2:DescribeInstances` required permissions:
		- Create an IAM role in the development accounts. 
		- Add the `ec2:DescribeInstances` permission to the role. 
		- Establish a trust relationship with the shared account for this role. 
		- Update the Lambda function IAM role in the shared account by adding the iam:AssumeRole permissions.
		- `iam:AssumeRole` -> used to assign permissions/policies
	- **Key Scenario:** Lambda invokes an action that is directed to another account/development account

#### Lambda
- If any async Lambda functions within a queue fail to process, always use a Dead Letter Queue for troubleshooting and reprocessing.
- If an application intends to invoke a Lambda function after a period of time (ex: 10 minutes) after an action (ex: account registration), use an **SQS Delay Queue** setting the Lambda function with the queue as the event source.
	- SQS Delay Queue delays the queued event for the specified time. In this case, once the account is registered in the application, an event is placed within the queue and is only executed once it's been alive for 10 minutes.
- If a **remote** Lambda function returns an Access Denied message, *update the Lambda function's execution role to include the missing permissions*.
- Printing to stdout via AWS Lambda sends the output to CloudWatch for logging
- Lambda Layers is used to package, load, and install dependencies. It allows separate management of dependencies, reducing the size of the deployment package. 
	- By moving large modules to a Lambda layers, only the dependencies used in the function are uploaded- speeding up the deployment process
	- **Key Scenario**: a new module/package added to the codebase is slowing down performance
- **Amazon EventBridge** can be used to schedule Lambda invocations (ex: every 10 minutes or so).
	- serverless
	- does not need extra management or additional infrastructure 
	- it runs naively, will always execute based on the set schedule without checking on any other factors
- If DynamoDB Data is throttled by data flow (in our case, by importing too much data via an document extraction Lambda function), it is best to have two Lambda functions instead: one for extracting and processing the data, another for uploading the extracted (and now smaller) data to the DynamoDB table, and an SQS queue in between to hold the output of the first function and deliver it to the second. This results in less data filling up the table.
- You can use Amazon Cognito Post Authentication to trigger a Lambda function after a user is successfully authenticated

#### CloudFormation 
- CloudFormation **change stack** is used to analyze changes (and how it will impact the resources) in the tech stack without the need to execute it.
	- useful for updating AWS CloudFormation stacks
- CloudFormation **stack policies** protects all resources in a stack by preventing stack resources from being unintentionally updated or deleted during a stack update. 
	- allows granular (specific) control over specific resources in a stack
	- only one stack policy per stack
- CloudFormation **resources** section declares the AWS resources that will be included in the stack (ex: EC2 instances or Amazon S3 bucket)
- CloudFormation **mappings** section matches a key to a corresponding set of values
	- useful for setting values based on region, etc.
- CloudFormation **transform** section declares macros to process the template in some way
	- macros can perform simple tasks like finding and replacing text, or they can make more extensive transformations to the entire template
	- executed in the specified order
- CloudFormation **conditions** section declares statements that define the circumstances under which entities are created or configured
	- You can create a condition and then associate it with a resource or output so that CloudFormation only creates the resource or output if the condition is true. 
	- Similarly, you can associate the condition with a property so that CloudFormation only sets the property to a specific value if the condition is true. If the condition is false, CloudFormation sets the property to a different value that you specify.
- CloudFormation **outputs** section declares output values that can be imported into another stack, return in response (to describe stack calls), or view in the CloudFormation console.
- If subnet referrals/imports in a CloudFormation template fail it can most likely be due to two reasons:
	- The template that owns the subnet did not export it in the Outputs section of the template
	- The developer template does not use the ImportValue intrinsic function to refer/import the subnets
	- **Key Scenario:** issues related to subnet imports/exports
	
#### AWS Serverless Application Model
- **AWS Serverless Application Model** CLI (AWS SAM) is a tool that helps developers build, test, and deploy serverless applications defined using the SAM template.
	- SAM is an extension of CloudFormation
	- Always bundle the application in a SAM package before deployment
	- Key Features:
		- **Local Development and Testing**
			- **Local Invoke**: Allows you to locally invoke Lambda functions, API Gateway endpoints, and other resources defined in your SAM template.
			- **Local Debugging**: Supports debugging Lambda functions locally using IDEs like Visual Studio Code.
		- **Packaging and Deployment**
			- **Packaging**: Packages your application and uploads artifacts (like Lambda function code) to an S3 bucket.
			- **Deployment**: Deploys your serverless application to AWS using AWS CloudFormation.
		- **Template Validation** validates your SAM templates to ensure they are syntactically correct and conform to the AWS SAM specification.
		- **Managing Application Stacks**: Facilitates the management of your application stacks and environments, enabling smooth transitions from development to production.
		- Generating Simple Projects
- Use **AWS Secrets Manager** with **SecureString** parameters If a developer wants to securely store the parameter values outside the code in an encrypted format and wants to turn on rotation for the credentials.
	- Keys:
		- SecureString (a feature of Secrets Manager Parameter Store): one-time fixed keys, securely store the parameter values outside the source
		- AWS Secrets Manager: rotate the credentials/secrets automatically
- To set up deployments to multiple environments with the least development effort in a serverless application using the AWS Serverless Application Model (AWS SAM), the developer can utilize a configuration file in TOML format with grouped configuration entries for each environment. This approach allows for easy management of different environment configurations and streamlines the deployment process.

#### AWS Secrets Manager
- To securely store credentials that an external SaaS API utilizes MOST securely: 
	- store them in AWS Secrets Manager, enable rotation, then configure the API to have Secrets Manager Access

#### AWS Key Management Store (KMS)
- When creating a DynamoDB table via AWS CLI, if no encryption setting is provided, it uses a default KMS managed key
- If a company needs to store all EC2 Lifecycle events in an SQS you can configure the permissions on main account event bus to receive alerts from all accounts.
- Amazon EC2 instances can send the state-change notification events to Amazon EventBridge.
- AWS App Config is a part of AWS System Manager designed for managing application configurations and feature toggles in a safe and controlled manner.
- Asymmetric Keys
	- not as suitable for automatic rotation
	- never leaves KMS unencrypted
	- Use cases:
		- where encryption is required outside of AWS by users who cannot call KMS
		- digital signatures
		- key pairs
	- Types:
		- RSA
		- Elliptic Curve
		- SM2
- KMS doesn't support automatic rotation for imported key material (key material brought in by the company)
#### ElastiCache
- Amazon ElastiCache can significantly increase read performance by caching frequently accessed data. 
	- This can reduce the load of an RDS database by serving previously stored query requests.
	- **Key Scenario**: performance degradation due to too many reads
- **Caching Strategies:**
	- **Write-through**: every write operation is simultaneously written to both the cache and the backing store (ex: a database)
		- best strategy for populating **real-time** dashboards using **ElastiCache**. when new data is written to the database, it is also written to the cache. (real-time)
	- **Write-behind**: write operations are first made to the cache, then the write is sent to the backing store asynchronously at a later time
	- **Read-through**: fetches data from the backing store if it is not already present in the cache
	- **Lazy-loading**: data is loaded into the cache ONLY when it is requested by the application. 
		- if the requested item is not in the cache, it is fetched from the backing store and then placed into the cache for future requests
- ElastiCache with Redis can easily implement a dashboard that keeps a list of sorted data by their rank. its also fast as fuck.
#### Miscellaneous
- When creating a partition key for a DynamoDB table, it is best to use the most unique attribute. This leads to efficient queries (pretty much no duplicates), and evenly distributed workloads across multiple database partitions. 
	- in the choice of Date, Username, and Account Status, username is the best choice due to it's uniqueness, distribution, and access patterns (better queries)
- DynamoDB has default encryption settings (most cost effective)
- When an ALB is used, the X-Forwarded-For header can be used to pass the client IP address to the applications backend servers
