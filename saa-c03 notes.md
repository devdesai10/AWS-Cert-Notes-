## Exam Prepper Notes
### this is notes throughout the entire exam prepper questions

A company containerized a windows job that runs on .NET 6 Framework under a Windows container. The company wants to run this job in the AWS cloud. The job runs every 10 minutes. The job's runtime varies between 1 minute and 3 minutes

Which solution is most cost-effective?  

#### Fargate
- Use Amazon ECS on the AWS Fargate to run the job. Create a scheduled task based on the container image of the job to run every 10 minutes

- By using ECS on AWS Fargate, you can run the job in a containerized environment while benefiting from the serverless nature of fargate, where you can only pay for the resource used during the job's execution. Creating a scheduled task based on the container image of the job ensures that it runs every 10 minutes, meeting the required schedule. This solution provides scalability, and cost effectiveness

#### Step Functions
- AWS Step Functions is a visual workflow service that helps developers use amazon web service to coordinate task into workflows

#### AppFlow
- Amazon Appflow is a fully managed integration service that enables you to securely transfer data between SaaS applications like Salesforce, Marketo, Slack, and ServiceNow, and AWS Services like Amazon S3 and Amazon Redshift
	- Can Securly transfer data between Salesforce and Amazon S3
	- Appflow supports encrypting data at rest in S3 using KMS CMKs
	- AppFlow supports encrypting data in transit using HTTPS/TLS  
	- Amazon Security Lake
	- Security group can only allow traffic inbound not outbound

#### RedShift
- Amazon Redshift - analyze structured and semi-structured data across data warehouses, operational databases, and data lakes

**Using AWS-designed hardware and machine learning to deliver the best price performance at any scale**

  
#### Proxy
- RDS Proxy - a fully managed, highly available, and easy to use database proxy feature of Amazon RDS

- • It makes it easy to connect to your RDS instances from applications running on AWS Lambda
- **• To reduce application failures resulting from database connection timeouts, the best solution is to enable RDS Proxy on the RDS DB Instance**

  
#### Athena
- **Amazon Athena** is an interactive query service that makes it easy to analyze data directly in S3 using standard SQL. 
- In a simple query we can apply Athena directly on the S3

  

Encrypting the data at the company's data center before storing the data in the s3 bucket would ensure that the data is encrypted in transit and at rest.

  

Network Load Balancer - Servers as the single point of contact for clients. Distributes incoming traffic across multiple targets, such as Amazon Ec2 Instances. WAN links, virtual machines, or servers, to avoid overloading any single host without using complex routing protocols

  

Application Load Balancer - For applications that use servers and serverless computing 

  

  

Amazon Macie is used to scan for vulnerabilities, but does not increase security.

  

Using KMS (Key Management Services) you can manage the keys as well as encrypt them making it a second form of security

  

An API Gateway is a software component that acts as a single entry point for application programming interface (API) calls to an application

Used for managing the cost effectiveness of app delivery and API integration 

  

Canary Release deployment, total API traffic is separated at random into a production release and a canary release with a preconfigured ratio. Typically, the canary release receives a small percentage of API traffic and the production release takes up the rest. The updated API features are only visible to API traffic through the canary. You can adjust the canary traffic percentage to optimize test coverage or performance.

- • In Short it is a strategy for gradually rolling out a new version of an application to a small group of users before making it available to a larger audience. (Beta Testing) 

  

  

If there are two VPCs and they use VPC peering connection to allow communication between the applications

What should you do to mitigate any single point of failure in the architecture

  

Add a second set of VPNs to the 1st VPC from a second customer gateway device

The VPC currently has a single VPN cionnection through one customer gateway device. THis is a single point of failure

Adding a second set of CPN Connections from the 1st VPC to a second customer gateway device provides redundancy and eliminates this single point of failure

  

Amazon inspector - helps you identify vulnerabilities within your ec2 instances and applications

  

When you hear SMB clients think of SMB protocols and that usually is the FSx Windows answer. 

  

Gateway Endpoint - Traffic between two services usually a VPC and EC2 or a S3 never leaves the Amazon network, so it doesnt have to traverse the internet. You can access the Amazon S3 without the need to use a NAT gateway or a VPN connection both use Internet.

  

Amazon QuickSight - to deliver easy to understand insights to the people who you work with, wherever they are.

  

Amazon Athena - Helps you analyze unstructured, semi structured, and structured data stored in Amazon S3

  

When there is a third party you want to ensure that they do not have access to the data before the data is encrypted and sent to AWS so you would use AWS KMS and then configure the application to store the archival files in the S3 bucket

  

Amazon Kinesis Data Stream - is a serverless streaming data service that makes it easy to capture, process, and store data streams at any scale.

  

You have to use us-east-1 region for ACM, and it should be public SSL/TLS for domain, in order for you to not incur any additional cost. 

  

Creating a Gateway Endpoint for Amazon S3 in the VPC. in the route tables for the private subnets, add an entry for the gateway endpoint. 

  

A gateway endpoint will also have no cost because the traffic will stay on the AWS infrastructure 

  

Service Control Policies (SCP) are polices that you attach to elements in an organization to manage permissions within that organization

  

Storage Lens - a cloud storage analytics feature that you can use to gain organization-wide visibility into object-storage usage and activity

**can also identify buckets that aren't following data-protection best practices, such as Replication or S3 Versioning**

  

If a company's target point object (RPO) is 5 minutes and the target recovery time objective (RTO) is 20 minutes. The company wants to minimize configuration changes. How would they do it with the **Most** operational efficiency

  

They would convert the Aurora Cluster to an Aurora Global Database, and the configure managed failover.

  

Glacier Instant Retrieval -> rarely accessed also it is 3 times lower compared to the Standard Infrequent Access. 

  

RDS Proxy is Serverless

  

Using Instance Scheduler on AWS to configure start and stop schedules will help optimize cost and reduce operational overhead based on the usage

**This would be helpful because your application receives traffic only on weekdays during business hours.**

  

Dynamo DB is NoSQL-JSON supported also using AWS Lambda is server-less so it has less operational overhead

  

Provisioned IOPS SSD Storage - highest performing Amazon EBS storage volumes designed for **critical, IOPS-intensive, and throughput-intensive workloads that require low latency**

  

If users report that they are receiving multiple emails for every uploaded image from the SQS messages are invoking the Lambda function more than once, which creates multiple email messages, then you have to increase the visibility timeout in the SQS queue to a value greater than the total of the function timeout and the batch window timeout 

**Lambda polls the message and starts processing the message.**

**However, before the first lambda can finish processing the message, the visibility timeout runs out on the SQS. It returns the message to the poll, causing another Lambda node to process the same message.** 

**By Increasing the visibility timeout, it should prevent the SQS from returning a message back to the poll before Lambda can finish processing the message** 

  

Elasticache is for memory and EFS is for durability

  

Lambda is fluctuating traffic patterns

  

AWS Systems Manager Run Command allows you to automate common admin tasks and perform one-time configuration changes at scale

  

Aurora cloning is beneficial for quickly setting up test environments using production data, without risking data corruption.

  

Anytime that a database is slowing down you need to create a read replica to offload the traffic

  

an interface gateway allows communication between resources in your VPC

  

You can not store images in a database

  

Running the Amazon Cloudwatch agent in the existing EKS cluster is called Amazon Cloudwatch container Insights

  

Lambda and SQS, when using SQS we will be sure that all images will be processed and hence to process we need 2 mins and 512 MB of memory ( Lambda allows upto 15 mins and upto 10K MB) Lambda should be perfect scalable solution which will allow for almost real-time image processing

  

If a company want elasticity and availabilty as som,e questions mention, so this leaves us in the two questions related to AUrora discarding the RDS MySQL Solution

  

Aurora cloning is especially useful for quickly setting up test environments using your production data, without risking data corruption.

  

Creating a read replica for the database. Configure the read replicas with the same compute and storage resources as the source database

Creating Read replicas allows the application to offload read traffic from the source database, improving its performance. The read replica should be configured with the same compute and storage resources as the source database to ensure that they can handle the read workload effectively

VPC gateway endpoint will allow no access to the internet, when your dealing with sensitive information

Creating a bucket policy that limits access to only the application tier running 

Read the questions for If it is a batch job or not because the questions with Lambda will fuck you up

Standard Infrequent is immediate + old shit (Immediate accesibility)

AWS Glue -> convert data to a file so it can be analyzed

AppFlow is a fully managed integration service that allows you to securely tansfer data between different SaaS (not the main function **Micro Services**)

SFTP - Secure File Transfer Protocol - a network protocol used for secure transfer of data over the internet

RDS Proxy - 

Convert to multi az for high availability and to eliminate single points of failure and minimize downtime 

Read replica - if a script on a database makes an app slow then make a read replica and run the script on there so it separates the compute

TCP / UDP = NLB (Network Load Balancer) 

SQS has a limit of 256 KB so using the extended client library will increase that limit

Compliance mode in Object Lock - No user, including the root user in an AWS account, can overwrite, delete, or alter object lock settings

Governance mode in Object Lock - Only users with special permissions can overwrite, delete, or alter object ock settings

Amazon Cognito - MFA or Authentication Service 

Multi AZ DB clusters are not available with the following engines:
	- RDS for MariaDB
	- RDS for Oracle
	- RDS for SQL Server

The key Advantages of Control Tower are that it is a fully managed service simplifies multi-account setup
	- Built-in account drift notifications detect OU changes automatically 
		- (This point is literally the answer and what the question is asking in this sense)

When you see scale seamlessly try to find the answers with Auto Scaling groups 

Route 53 has a feature DNS failover when instances go down so we dont need to use CloudWatch or Lambda to trigger 

When in the context of migrating a Windows internet Information Service web application to AWS, the best storage option would be to **Migrate the file share to Amazon FSx for Windows File Server** 
- An RDS is a database service so it would not make sense to use it for the storage solution
- Storage Gateway is a hybrid cloud storage service that connects on-premises applications to AWS storage service (Not migrating from windows to AWS)
- EFS though it looks like one of the best options, provides a shared file storage for Linux-based workloads, but it does not natively support Windows-based workloads

Amazon Macie is designed specifically for discovering and classifying sensitive data like PII in S3. Whenever you hear PII think Macie 
Macie can be enabled directly in the required regions rather than enabling it across all regions which is unnecessary. This minimizes overhead

To secure access to a bucket configuring a VPC gateway endpoint would make it so that it does not have to travel through the internet. 

Creating a bucket policy would secure access and only allow the VPC application tier to access it

Gateway endpoints do not allow access from on-premises networks, from peered VPCs in other AWS regions, Interface endpoints allow this for an additional cost

**Interface Endpoint** enables connectivity to a wider range of services, while Gateway endpoints are specifically designed for routing traffic to S3 and Dynamo DB

When experiencing a application that performs slowly when traffic increases, this coming from a heavy read load during periods of high traffic, this means you should create a read replica for the DB instance and then send traffic to the read replica. also create a ElastiCache cluster to cache query results in the cluster

#### SCT vs DMS
Amazon Schema Conversion Tool (SCT) - to convert SQL in your C++, C#, Java, or other application code

The difference between SCT and DMS is
	- DMS traditionally moves smaller relational workloads (<10TB)
	- SCT is primarily used to migrate large Data warehouse workloads

#### S3 Access Point
- An Amazon S3 Access Point is a feature that simplifies managing data access at scale for applications using shared data sets in Amazon S3. Access Points are uniquely named network endpoints that are **attached to a bucket and enforce distinct and precise permissions and network controls for any request made through the access point.**
	By creating separate access points for each application, you can enforce access controls specific to their respective prefixes while minimizing administrative complexity. This approach provides a clean separation of permissions and reduces the risk of misconfigurations

Using the direct option on anything will usually be the right answer 
**A company wants to send all AWS systems manager session manager logs to an Amazon S3 bucket for archival purpose**
	- In this situation you would enable S3 logging in the systems manager console, and choose the S3 bucket to send the session data to.
	- This would be the MOST operational efficiency

### A company wants to migrate an on-premises data center to AWS. The data center hosts a storage server that stores data in an NFS-based file system. The storage server holds 200 GB of data. The company needs to migrate the data without interruption to existing services. Multiple resources in AWS must be able to access the data by using NFS protocol. 

#### Elastic File System (EFS)
provides a scalable, high-performance NFS file system that can be accessed from multiple resources in AWS. 

#### AWS DataSync 
can perform the migration from the on-premises NFS server to EFS without interruption to existing services.

This avoids having to manually move the dat which could cause downtime. DataSync incrementally syncs changed data. EFS and DataSync together provide a cost-optimized approach compared to using S3 or FSx, while still meeting the requirements. Manually copying 200GB of data to AWS would be slow and risky compared to using DataSync


### a company runs workloads on AWS. The company needs to connect to a service from an external provider. The service is hosted in the provider's VPC. according to the company's security team, the connectivity must be private and must be restricted to the target service. The connection must be initiated only from the company's VPC

#### VPC Endpoint
The VPC endpoint ensures that the application does not transverse the internet. Connects you to service hosted by AWS Partners and supported solutions available in the AWS marketplace

#### AWS PrivateLink
provides private connectivity between VPCs, AWS services, and on-premises networks, without exposing your traffic to the public internet. AWS PrivateLink makes it easy to connect services across different accounts and VPCs to significantly simplify your network architecture. 

By asking the provider to create a VPC endpoint for the target service, the company can use PrivateLink to connect to the target service. This enables the company to access the service privately and securely over an Amazon VPC endpoint, without requiring a NAT gateway, VPN, or AWS Direct Connect. Additionally, this will restrict the connectivity only to the target service, as required by the company's security team. 

### What is a Virtual Private Gateway?
a tool that creates a secure tunnel to transport encrypted data between devices, the cloud, and enterprise servers across the **internet**

### A company's website provides users with downloadable historical performance reports. the website needs a solution that will scale to meet the company's website demands globally. The solution should be cost-effective, limit the provisioning of infrastructure resources, and provide the fastest possible response time. 

#### Amazon CloudFront and Amazon S3
When hearing historical performance reports this means its static content. which is S3. This solution is cost-effective, limit the provisioning of infrastructure resources, and provides the fastest possible response time. 

### A company has seperate AWS accounts for its finance, data analytics, and development departments. Because of costs and security concerns, the company wants to control which services each AWS account can use.  (Least operational overhead)

#### Organization Unites (OUs)
When you see this in this question you should think about departments which is also in the question. 
#### Service Control Policies (SCPs)
a type of organization policy that can be used to manage permissions for users and roles in an organization. In this question you use SCPs to centralize permissions and allow the departments to only use what they need

### A manufacturing company has machine sensors that upload .csv files to an Amazon S3 bucket. These .csv files must be converted into images and must be made available as soon as possible for the automatic generation of graphical reports

### The images become irrelevant after 1 month, but the .csv files must be kept to train Machine Learning (ML) models twice a year. The ML trainings and audits are planned weeks in advance. (MOST COST EFFECTIVE)

#### For processing the image
Use Lambda as its is very cost efficient and more cost efficient that EC2 Spot Instances
- Design an AWS Lambda function that converts the .csv files into images and store the images in the S3 bucket. Invoke the Lambda function when the .csv file is uploaded

#### Photo and file management
for expiring images after 30 days and because the ML trainings are planned weeks in advance S3 Glacier is ideal for slow retrieval and cheap storage
- Create S3 Lifecycle rules for .csv files and image files in the S3 bucket. Transition the .csv files from S3 Standard to S3 Glacier (Because once the csv file is converted then they aren't needed until the ML trainings which are twice a year). Expire the image files after 30 days. (This would get rid of the images and not incur storage cost because the images become irrelevant after 1 month)

### A company is building a three-tier application on AWS. The presentation tier will serve a static website The logic tier is a containerized application. This application will store data in a relational database. The company wants to simplify deployment and to reduce operational costs. 

#### S3 
S3 is for the Static website so it eliminates the other options without S3.

#### ECS (Elastic Container Service)
The reason why we chose ECS instead of EKS is because EKS is a little more expensive than ECS but it is still cheaper and the company wants to simplify and reduce cost

#### RDS 
This is the answer because they want a relational database

### Use Amazon Elastic Kubernetes Service (Amazon EKS) with Amazon EC2 worker nodes. A company has deployed an application in an AWS account. the application consist of microservices that run on AWS Lambda and Amazon Kubernetes Service (EKS). A separate team supports each microservice. The company has multiple AWS accounts and wants to give each team its own account for its microservices 

#### VPC Lattice
a fully managed application networking service that helps connect, secure, and monitor application services. You can use Lattice with a single virtual private cloud, or across multiple VPCs from one or more accounts.
- is a completely new way to simplify API communication between services or microservices in one or more AWS accounts 

### A company is using a centralized AWS account to store log data in various Amazon S3 buckets. A solutions architect needs to ensure that the data is encrypted at rest before the data is uploaded to the S3 buckets. The data also must be encrypted in transit.

#### Client-side encryption 
the keyword here is **before** the data is encrypted at rest before the data is uploaded to the S3 buckets
client-side encryption can be at rest or can be in transit. meaning that the last sentence is there to throw you off.

### A solutions architect runs a web application on multiple Amazon EC2 instances that are in individual target groups behind an application load balancer (ALB). Users can reach the application through a public website.

### The solutions architect wants to allow engineers to use a development version of the website to access one specific development EC2 instance to test new features for the application. The solutions architect wants to use an Amazon Route 53 hosted zone to give the engineers access to the development instance. The solution must automatically route to the development instance even if the development instance is replaced.

#### A Record (Alias Record)


### A media company uses an Amazon CloudFront distribution to deliver content over the internet. The company wants only premium customers to have access to the media streams and file content. The company stores all content in an Amazon S3 Bucket. The Company also delivers content on demand to customers for a specific purpose, such as movie rentals or music downloads.

#### CloudFront signed URLs
is just a different url but holds different information. Something that can be changed between premium users and free users

### A company wants to monitor its AWS costs for financial review. The cloud operations team is designing an architecture in the AWS Organizations management account to query AWS Cost and Usage Reports for all member accounts. The team must run this query once a month and provide a detailed analysis of the bill.

#### Amazon Athena 
Athena is a query and data analysis database which means that it would probably be this answer. For this question you will need to enable Cost and Usage Reports regardless.

### A company runs a Java-based job on an Amazon Ec2 Instance. The job runs every hour and takes 10 seconds to run. The job runs on a scheduled interval and consumes 1 GB of memory. The CPU utilization of the instance is low except for short surges during which the job uses the maximum CPU available. The company wants to optimize the costs to run the job

#### Lambda Function and then EventBridge
The reason that this is Lambda first of all is because Lambda has a memory capacity of around 10 GBs while the question is asking for 1 GB.
	Lambda allows you to allocate memory for your functions in increments of 1 MB, ranging from a minimum of 128 MB to a maximum of 10,240 MB (10GB)

### An application runs on Amazon Ec2 instances in private subnets. the application needs to access tan Amazon DynamoDB table. What is the MOST secure way to access the table while ensuring that the traffic does not leave the AWS network? 

#### VPC Endpoint
This is very simple you set up a VPC endpoint in order to not have it traverse the internet.
VPC endpoints ensure private and secure access to the DynamoDB table from your EC2 instances in the private subnets, without the need to traverse the internet or leave the AWS network.

### A company host an application used to upload files to an Amazon S3 bucket. Once uploaded, the files are processed to extract metadata, which takes less than 5 seconds. The volumes and frequency of the uploads varies from a few files eahc hour to hundreds of concurrent uploads. The company has asked a solutions architect to design a cost-effective architecture that will meet these requirements. 

#### Object-created event notifications
While Amazon SNS (Simple Notification Service) might be the first thing that you think of, it can be used to trigger actions based on S3 events, its not directly involved with processing files. Where object-created event notifications are a feature that enables you to receive notifications when certain events occur in your S3 bucket, specifically when objects are created. This allows you to automate workflows and trigger actions in response to changes in your bucket.

### A company creates dedicated AWS accounts in AWS organizations for its business units. Recently, an important notification was sent to the root user email address of a business unit account instead of the assigned account owner. The company wants to ensure that all future notifications can be sent to different employees based on the notification categories of billing, operations, or security.

#### Use Email Aliases. 
Configuring each AWS account's root user to use email aliases that go to a centralized mailbox ensures that sensitive notifications are not directly sent to individual email addresses. Instead they are directed to a centralized mailbox, reducing the risk of unauthorized access to sensitive information. additionally, configuring alternate contacts for each account using a single business-managed email distrubution list for the billing team, the security team, and the operations team ensures that notifications are appropriately routed to the respective teams based on the categories of billing, operations, or security. This approach centralizes control and reduces the likelihood of misconfiguration or unauthorized access to sensitive notifications
	**This is the most secure solution for ensuring that future notifications can be sent to different employees based on the notification categories of billing, operations, or security**

### A company wants to ingest customer payment data into the company's data lake in Amazon S3. the company receives payment data every minute on average. The company wants to analyze the payment data in real time. Then the company wants to ingest the data into the data lake. (MOST operational efficient)

#### Amazon Kinesis Data Firehouse
Firehose is near real time (min. 60 sec). This is the process that ingest informations to be analyzed
#### Amazon Kinesis Data Streams
This is the service that deals with storing the information that needs to be analyzed
#### Amazon Kinesis Data Analytics
This is the service that processes analysis

### An ecommerce company wants to launch a one-deal-a-day website on AWS. Each day will feature exactly one product on sale for a period of 24 hours. The company wants to be able to handle millions of request each hour with millisecond latency during peak hours (LEAST operational overhead)

#### Scalability
The solution would be, Use an Amazon S3 bucket to host the website's static content. Deploy an Amazon CloudFront distribution. Set the S3 bucket as the origin. Use Amazon API gateway and AWS Lambda functions for the backend APIs. Store the data in Amazon DynamoDB. 
	Using S3 to host static content and CloudFront to distribute the content can provide high performance and scale for websites with millions of request each hour. Amazon API gateway and AWS Lambda can be used to build scalable and highly available backend APIs to support the website, and the Amazon DynamoDB can be used to store the data. This solution requires minimal operational overhead as it leverages fully managed services that automatically scale to meet demand.

### A solutions architect is designing a new service behind Amazon API gateway. The request patterns for the service will be unpredictable and can change suddenly from 0 request to over 500 per second. The total size of the data that needs to be persisted in a backend database is currently less than 1 GB with unpredictable future growth. data can be queried using simple key-value requests. 

#### AWS Lambda
The reason is because of the keywords unpredictable request patterns, scalable
#### Amazon DynamoDB
The reason for Dynamo is because the key-value data, scalable 

### A solutions architect is designing a security solution for a company that wants to provide developers with individual AWS accounts through AWS Organizations, while also maintaining standard security controls. Because the individual developers will have AWS account root user-level access to their own accounts, the solutions architect wants to ensure that the mandatory AWS CloudTrail configuration that is applied to new developer account is not modified

#### Service Control Policy (SCP)
The reason why is the keywords Organizations + restricts 
### A company host more than 300 global websites and applications. The company requires a platform to analyze more than 30 TB of clickstream data each day. What should a solutions architect do to transmit and process the clickstream data? 

#### Transmitting and Processing Clickstream Data
Amazon Kinesis Data Streams is a highly scalable and durable service that enables real-time processing of streaming data at high volumes and high rate. You can use Kinesis Data Streams to collect and process the clickstream data in real-time. 
Amazon Kinesis Data Firehose is a fully managed service that loads streaming data into data stores and analytics tools. You can use Firehose to transmit the data from Data Streams to an Amazon S3 Data Lake

### A company has an AWS lambda function that needs read access to an Amazon S3 bucket that is located in the same AWS account (MOST secure manner)

#### IAM Role
- An IAM role provides temporary credentials to the Lambda function to access AWS resources. The function does not have persistent credentials
- The IAM policy grants least privilege access by specifying read access only to the specific S3 bucket needed. Access is not granted to all the S3 buckets
- If the Lambda function is compromised, the attacker would only gain access to the one specified S3 bucket. They would not receive broad access to resources.

### A company stores raw collected data in an Amazon S3 bucket. the data is used for several types of analytics on behalf of the company's customers. The type of analytics requested determines the access pattern on the S3 object (Company wants to reduce cost)

#### Intelligent Tiering
Unpredictable access patterns means intelligent tiering

### A company runs a shopping application that uses Amazon DynamoDB to store customer information. In case of data corruption, a solution architect needs to design a solution that meets a recovery point objective (RPO) 15 minutes and a recovery time objective (RTO) of 1 hour.

#### Point in time Recovery
designed as a continuous backup just to recover it fast. It covers perfectly the RPO, and probably the RTO

### A company uses on-premises servers to host its applications. The company is running out of storage capacity. The applications use both block storage and NFS storage. The company needs a high-performing solution that supports local caching without re-architecting its existing applications.

#### AWS Storage Gateway
By combining the deployment of an AWS Storage Gateway file gateway and an volume gateway, the company can address both its block storage and NFS storage needs, while leveraging local caching capabilities for improved performance
- Both use Storage Gateway which can be used as NFS and Block Storage

### A Company is moving it data management application to AWS. The company wants to transition to an event-driven architecture. The architecture needs to be more distributed and to use serverless concepts while performing the different aspects of the workflow. The company also want to minimize operational overhead.

#### Serverless
The architecture needs to be distributed and to use serverless concepts, Step functions and Lambda are both serverless 

### An online learning company is migrating to the AWS cloud. The company maintians its student records in a Postgre SQL database. The company needs a solution in which its data is available and online across multiple AWS regions at all times

#### read replica in another region
because this question ask for a different region Multi-AZ is not the right answer, but a read replica would work in this situation but in another Region would be beneficial

### A Company recently migrated to AWS and wants to implement a solution to protect the traffic that flows in and out of the production VPC. The company had an inspection server in its on-premises data center. The inspection server performed specific operations such as traffic flow inspection and traffic filtering. The company wants to have the same functionalities in the AWS Cloud.

#### AWS Network Firewall
Network firewall is a managed firewall service that provides filtering for both inbound and outbound network traffic. It allows you to create rules for traffic inspection and filtering, which can help protect your production VPC.
- In this situation you use Network Firewall to create the required rules for traffic inspection and traffic filtering for the production VPC

### A Gaming company wants to launch a new internet-facing application in multiple AWS Regions. The Application will use the TCP and UDP protocols for communication. The company needs to provide high availability and minimum latency for global users.

#### Network Load Balancers
Because of the TCP and UDP part
#### Global Accelerator
Because of the need to provide high availability and minimum latency for global users 

### A company is migrating five on-premises applications to VPCs in the AWS Cloud. Each application is currently deployed in isolated virtual networks on premises and should be deployed similarly in the AWS Cloud. The applications need to reach a shared services VPC. All the applications must be able to communicate with each other

#### Transit Gateway 
It will allow for inter-VPC communication for all 5 applications/VPC, reach shared resource/VPC and in the future it will be easy to allow for inter-communication between even 100 VPCs (applications)

### A company host a website on Amazon EC2 instances behind an Application Load Balancer (ALB). The website servers static content. Website traffic is increasing. The company wants to minimize the website hosting costs. 

#### S3 and CloudFront
Static Content usually means S3, But Amazon CloudFront: uses the durable storage of Amazon Simple Storage Service (Amazon S3) - this solution creates an Amazon S3 Bucket to host your static website's content. To update your website, just upload your new files to the S3 Bucket

### A company creates operation data and stores the data in an Amazon S3 bucket. For the company's annual audit, an external consultant needs to access an annual report that is stored in the S3 bucket. The external consultant needs to access the report for 7 Days. The company must implement a solution to allow the external consultant to access to only the report. (MOST operation efficiency)

#### Presigned URL
When using CLI to create a presigned URL we can setup 7 days for URL expiration from the time of the creation
Pre-signed URLs are used to provide short-term access to a private object in your S3 bucket. They work by appending an AWS Access Key, expiration time, and Sigv4 signature as query parameters to the S3 Object.

### A company has deployed a multi-account strategy on AWS by using AWS control tower. The company has provided individual AWS accounts to each of its developers. The Company wants to implement controls to limit AWS resource costs that the developers incur. (LEAST operational overhead)

#### AWS Budgets 
Taking into consideration that AWS Budgets is allowing to inform you that you exceeded budged and execute actions like for example IAM actions to prevent running new resources in cloud, I think this option is a good reasonable move. In case of need Budged can be always increased and "chains" disabled

### A company is storing sensitive user information in an Amazon S3 bucket. The company wants to provide secure access to this bucket from the application tier running on Amazon EC2 Instances inside a VPC

#### VPC Gateway and Bucket Policy
VPC gateway - for direct connection (no public internet) to access S3 
Bucket Policy - to secure access and only allow the VPC application tier to access it

### A company host an application on Amazon EC2 instance that run in a single AZ. The application is accessible by using the transport layer of the Open Systems Interconnection (OSI) model. The company needs the application architecture to have high availability (MOST cost effective)

#### Auto Scaling Group and Network Load Balancer
Network Load Balancer - The application is accessible by using the transport layer, which is TCP
Auto Scaling - because the architecture needs to be scalable it makes it much more available

### A company uses a Microsoft SQL Server database. The company's applications are connected to the database. The company wants to migrate to an Amazon Aurora PostgreSQL database with minimal changes to the application code.

#### SCT & DMS 
Since you dont need to rewrite the SQL queries it doesn't make sense 

#### Babelfish
is a new capability for Amazon Aurora PostgreSQL-Compatible edition that enables Aurora to understand commands from applications written for Microsoft SQL Server

### A company host an application on AWS Lambda functions that are invoked by an Amazon API gateway API. The Lambda functions save customer data to an Amazon Aurora MySQL database. Whenever the company upgrades the database, the Lambda function fail to establish database connections until the upgrade is complete. The result is that customer data is not recorded for some of the event. 

#### Amazon SQS 
The SQS queue with the retention time is reasonably longer than the upgrade time, so if the Lambda function times out, the data will remain in the queue until it is successfully inserted into the DB later and then removed from the queue

### A company has two AWS accounts: production and Development. The company needs to push code changes in the development account to the Production account. In the alpha phase, only two senior development team need access to the production account. In the beta phase, more developers will need access to perform testing. 

#### IAM role in the Production Account
create the IAM role in the production account and the create a trust policy that specifies that the development account. this allows developers to assume the role

### A company runs an on-premises application that is powered by a MySQL database. The company is migrating the application to AWS to increase the application's elasticity and availability. The current architecture shows heavy read activity on the database during times of normal operation. Every 4 hours the Company's development team pulls a full export of the production database to populate a database in the staging environment. During this period, users experience unacceptable application latency. The development team is unable to use the staging environment until the procedure completes. 

#### Use Amazon Aurora MySQL with Multi-AZ Aurora Replicas for production. Use database cloning to create the staging database on-demand
This allows the development team to continue using the staging environment without delay, while also providing elasticity and availability for the production application.

### A company runs its application by using Amazon EC2 Instances and AWS Lambda functions. The EC2 Instance run in private subnets of a VPC. The Lambda functions need direct network access to the Ec2 instances for the application to work.
### the application will run for 1 year. The number of Lambda functions that the application uses will increase during the 1-year period. The company must minimize costs on all application resources

#### Purchasing a Compute Savings Plan
The connecting the Lambda functions to the private subnets that contain the EC2 instances
	This plan offers significant discounts on Lambda functions compared to on-demand pricing. Since the application will run for a year, a sustained use discount like Compute Savings plan is ideal. 
	Private Subnets: Lambda functions in private subnets can directly access EC2 instances within the VPC without needing internet access, reducing security risk and potential egress cost.

### A company wants to enhance its ecommerce order-processing application that is deployed on AWS. The application must process each order exactly once without affecting the customer experience during unpredictable traffic surges.

#### Amazon SQS FIFO
Must process each order exactly once -> FIFO Queue (First in First Out)

### A company host its application in the AWS cloud. the application runs on Amazon EC2 instance in an auto scaling group behind an ELB load balancer. The application connects to an Amazon DynamoDB table. For disaster recovery purposes, the company wants to ensure that the application is available from another AWS region with minimal downtime. (LEAST Downtime)

#### Create an Auto scaling group and an ELB in the DR Region.
Configure the DynamoDB table as a global table. Configure DNS failover to point to the new DR Region's ELB
	With Dynamo global tables, we just need to create an ELB and a ASG in the DR region resources. This resources will be used only if the main region fail over.

### A company plans to run a hgih performance computing (HPC) workload on Amazon EC2 instances. The workload requires low-latency network performance and high network throughput with tightly coupled node-to-node communication

### Cluster Placement Group
Tightly couple, low latency, hpc, usually means cluster placement group

### A company runs several Amazon RDS for Oracle On-Demand DB instances that have high utilization. The RDS DB instances run in member accounts that are in an organization in AWS Organizations

### the company's finance time has access to the organization's management account and member accounts. The finance team wants to find ways to optimize costs by using AWS Trusted Advisor

#### Use the trusted advisor recommendations in the management account
#### use the trusted advisor checks for Amazon RDS reserved instance optimization

### A company is hosting a high-traffic static website on S3 with an CloudFront distribution that has a default TTL of 0 seconds. the Company wants to implement caching to improve performance for the website. However, the company also want to ensure that stale content is not served for more than a few minutes after a deployment

#### Set the CloudFront default TTL to 2 minutes
#### add a cache control max-age directive of 24 hours to the objects in S3. On deployment, create a CloudFront invalidation to clear any changed files from edge caches

If you min TTL is greater than 0, cloud front uses the cache policy's minimum TTL, even if the Cache-control: no-cache, no-store, and/or private directives are present in the origin headers

### A company runs its critical storage application in the AWS Cloud. The application uses S3 in two AWS Regions. The Company wants the application to send remote user data to the nearest S3 bucket with no public network congestion. The company also wants the application to fail over with the least amount of management of S3.

#### Set up S3 to use Multi-Region Access Points in an active-active configuration with a single global endpoint. Configure S3 Cross-Region Replication
using a multi-region access point in an active-active setup will send data to the closest region, without accessing the internet 

### A company plans to rehost an application to Amazon Ec2 Instances that use Amazon EBS as the attached storage. A SA must design a solution to ensure that all newly created EBS volumes are encrypted by default. The solution must also prevent the creation of unencrypted EBS volumes

#### Configure the EC2 account attributes to always encrypt new EBS volumes 
the task is to force automatic encryption on every new EBS volume and prevent possibility of creation any unencrypted volumes 

### An application allows users at a company's headquarters to access product data. The product data is stored in an Amazon RDS MySQL DB instance. The operations team has isolated an application performance slowdown and wants to separate read traffic from write traffic. A solutions architect needs to optimize the application's performance quickly

#### Create read replicas for the databases. Configure the read replicas with the same compute and storage resources as the source database
creating read replicas allows the application to offload read traffic from the source database, improving the performance. The read replica should be configured with the same compute and storage resources as the source database to ensure that they can handle the read workload effectively

