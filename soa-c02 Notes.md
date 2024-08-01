# CloudFront
- Amazon CloudFront is a Content Delivery Network
	**CloudFront** uses a globally distributed network of proxy servers (**Edge Locations**) to cache content, such as **web pages, images, videos, and applications**. 
### **Key Benefits**
**Improved Performance** 
	Delivers content faster by reducing latency
**Increased Scalability**
	handles large amounts of traffic and sudden spikes
**Reduced Costs**
	Optimizes bandwidth usage and reduces origin server load
**Enhanced Security**
	Protects content with SSL/TLS encryption and other security features
**Global Reach**
	 Delivers content to users worldwide with low latency
### **Common Use Cases**
- **Static Content delivery**: Serving images, CSS, JavaScript, and other static assets
- **Video Streaming**: Delivering high-quality videos with low buffering
- **Application acceleration**: Improving the performance of web applications
- **API distribution**: Delivering APIs with Low Latency
### **Important Concepts Related to CloudFront**
- ### Origin: 
	The source of your content (S3, EC2, Elastic Load Balancing, etc.)
- ### Distribution: 
	A Group of edge locations that serve your content
- ###  Edge Locations: 
	a physical location where CloudFront stores cached content
- ### Invalidation: 
	a process to remove cached content from edge locations
	
	**By default, CloudFront caches a response from Amazon S3 for 24 hours (Default TTL of 86,400 seconds) if your request lands at an edge location that served the Amazon S3 response within 24 hours, then CloudFront uses the cached response. This happens even if you updated the content in Amazon S3** 
	
- ### Price Class:
	determines the price you pay for data transfer

# Origin Access Identity (OAI)
An Origin Access Identity (OAI) is a special CloudFront user that you can associate with your Amazon S3 origins to secure your content.
### Why use an OAI?
- #### Security
	By using an OAI, you can restrict access to your S3 content to only CloudFront. this prevents unauthorized access to your content through direct S3 URLs.
- #### Control
	You have granular control over which CloudFront distributions can access your S3 content. 
### Key points to remember
- An OAI is required if you want to serve private content from an S3 bucket using CloudFront
- You can associate multiple OAIs with a single S3 bucket
- OAIs are not required for public S3 buckets

# Cache-Control Header
- **The Cache-Control header is an HTTP header that instructs browsers and intermediate caches (like CDNs) on how to handle caching of a resource.** It's used to control caching behavior in both client request and server response.
### How it works
	The header consist of directives thats specify caching rules. Common directives include
- **max-age**: Defines the maximum age of a cached resource in seconds.
	[TTL is something different; its not for caching]
- **no-cache**: Indicates that the resource should not be cached, but the cache can store the response with a new request to validate it 
- **no-store**: Prohibits caching of the response, including intermediate caches
- **public**: Indicates that the response can be cached by any cache 
- **private**: Indicates that the response can only be cached by the client
- **must-revalidate**: The cache must validate the resource with the origin server before using it again
#### Importance of Cache-Control
- **Improved Performance**
	By effectively using caching, you can reduce server load, improve website speed, and enhance user experience
- **Bandwidth Optimization**
	Caching reduces data transfer, saving bandwidth costs
- **Content Freshness**
	You can control how often content is refreshed by setting appropriate cache expiration times


# Amazon Machine Images (AMI)
- **An amazon machine image is essentially a template used to create instances (virtual machines) on Amazon EC2** Its like a blueprint for your virtual server
#### Components of an AMI:
- **Root volume template:**
	includes the operating system (like Linux, Windows), applications and configuration settings
- **Launch Permissions:**
	Specifies which AWS accounts can use the AMI to launch instances
- **Block device mapping**
	Defines the volumes to attach to the instance when it's launched
#### How it Works
- When you launch an instance from an AMI, EC2 creates a copy of the AMI and uses it to boot up your instance. This process is relatively fast, allowing you to quickly provision new servers
#### Benefits of AMIs
- **Speed and efficiency:**
	Quickly launch instances with preconfigured software
- **Consistency**
	Ensures consistent environments across multiple instances
- **Cost-effective**
	Reuse AMIS for multiple instances, reducing setup time
- **Flexibility**
	Choose from a wide variety of AMIs, including public, private, and marketplace options

# NAT Gateways
- **A NAT Gateway is a Network Address Translation (NAT) service that allows instances in a private subnet to connect to the internet while preventing external services from initiating connections to those instances**
#### How it Works:
- Outbound Traffic
	When an instance in a private subnet needs to access the internet, it sends traffic to the NAT Gateway
- Translation
	The NAT Gateway translates the private IP address of the instance to it own public IP Address
- Internet Access
	The traffic is then routed to the internet using the public IP address
- Inbound Traffic
	The NAT Gateway only allows inbound traffic that is a direct response to an outbound connection initiated by an instance in the private subnet
#### Key Benefits
- Enhanced Security
	Protects instances in private subnets from direct internet access
- Simplified Network Configuration
	Eliminates the need for public IP addresses for instances in private subnets
- High Availability
	NAT Gateways are highly available to ensure uninterrupted connectivity
#### In Use
- A SysOps administrator migrates NAT instances to NAT gateways. After the migration, an application that is hosted on Amazon EC2 instances in a private subnet cannot access the internet
- What of the following are possible reasons for this problem
	- **NAT Gateway is not in the Available State**
		NAT Gateway itself has issues or not yet ready
	- **The application is using a protocol that the NAT Gateway does not support**
		NAT Gateway does not support IPv6

# Amazon S3 gateway endpoint
- An Amazon S3 gateway endpoint provides private access to S3 from within your VPC without requiring an internet gateway or NAT device. This means your traffic stays within the AWS network, enhancing security and performance
#### How it works
- **Create a Gateway Endpoint:** You create a gateway endpoint for S3 in your VPC
- **Configure Route Tables**: You add a route to the route table of your subnets, directing S3 traffic to the gateway endpoint
- **Access S3:** Instances in your VPC can now access S3 without needing to go through the public internet
#### Benefits
- Enhanced Security
	Isolates your S3 traffic within the AWS Network
- Improved Performance
	Lower latency compared to going through the internet
- Cost Savings
	Eliminates the need for internet gateways or NAT devices
#### In Use
- A SysOps Administrator configures an Amazon S3 gateway endpoint in a VPC. The private subnets inside the VPC do not have outbound internet access. User logs in to an Amazon Ec2 Instance in one of the private subnets and cannot upload a file to an Amazon S3 bucket in the same AWS Region\
- Update the S3 bucket policy to allow s3:PutObject access from the private subnet CIDR block
	**When an Amazon S3 gateway endpoint is configured in a VPC, the private subnets within the VPC need to have their route tables updated to route the S3 traffic to the gateway endpoint, instead of the internet
	Without the appropriate route table updates, the EC2 instance in the private subnet will be able to communicate with the S3 bucket, even if the instance has the necessary S3 permissions.

# Service Control Policy (SCP)
- **A Service control policy is a type of organizational policy in AWS Organizations that sets limits on the actions IAM users and roles can perform.**
- It acts as a guardrail, preventing users from exceeding certain permissions
### How it works
- Centralized Control:
	SCPs are applied at the organization or Organizational Units (OU) level, affecting all accounts within that scope
- Permission limits
	SCPs define the maximum permissions allowed, but they don't grant permissions themselves
- Intersection of Permissions
	The effective permissions for a user or role are the intersection of the SCP, IAM policies, and resource-based policies

### Key benefits
- Enforced Compliance
	helps maintain security and compliance standards across the organization
- Risk Mitigation
	Reduce the risk of unauthorized actions by limiting permissions
- Improved Governance
	Provides a centralized way to manage permissions

### Common Use Cases
- Preventing Resource Sharing
	Limiting which accounts can share resources
- Restricting Service Usage
	Prohibiting the use of certain AWS services
- Limiting Spending:
	Setting spending limits for AWS accounts
- Enforcing Security best practices
	Ensuring adherence to security standards

### In Use
- A Company wants to prohibit its developers from using a particular family of Amazon EC2 Instances. The company uses AWS Organizations and wants to apply the restriction across multiple accounts
- What is the MOST operationally efficient way for the company to apply service control policies (SCPs) to meet these requirements

	**Add the accounts to an organizations unit (OU). Apply the SCPs to the OU**
	The Question says MOST operationally efficient. If they do not already use CT it adds another layer of complexity. They will still need to create OU's for the Developers anyway

# CloudTrail
- CloudTrail is a service that provides a record of actions taken in your AWS account
- It records API calls for your AWS account and delivers log files to an S3 bucket

### How it Works
- API Call Recording
	Cloud Trail records API calls made by users, roles, and AWS services
- Log Delivery
	The recorded data is delivered as log files to an S3 bucket of your choice
- Data Retention
	You can configure Cloud Trial to retain log files for a specified period
- Integration with other services
	CloudTrail integrates with other AWS services like CloudWatch Logs, Lambda, and Kinesis Data Firehouse for further analysis and processing

### Key Benefits
- Security and Compliance
	Helps monitor for suspicious activity and meet compliance requirements
- Troubleshooting
	Provides insights into system behavior for troubleshooting issues
- Cost Optimization
	Identifies opportunities to reduce costs by analyzing resource usage
- Auditing
	records changes to AWS resources for auditing purposes

### In Use
- A company store critical data in Amazon S3 buckets. A SysOps Admin must build a solution to record all S3 API activity. 
	- Create an AWS CloudTrail trail to log data events for all S3 Objects
	**Amazon S3 is integrated with AWS CloudTrail, a service that provides a record of actions taken by a user, role, or an AWS service in Amazon S3. CloudTrail captures a subset of API calls for Amazon S3 as events, including calls from the Amazon S3 console and code calls to the Amazon S3 API**

# CloudWatch 
- AWS CloudWatch is a monitoring and logging service that provides data on AWS resources.
- It helps you collect and track metrics, logs, and events
### How it Works
- Data Collection
	CloudWatch collects metrics, logs, and events from your AWS resources
- Data Storage
	The collected data is stored in CloudWatch for analysis and visualization
- Alarms and Notifications
	You can set alarms based on metrics and receive notifications when thresholds are breached
- Data Visualization
	CloudWatch provides dashboards and graphs for visualizing data
### Key Benefits
- Monitoring AWS Resources
	Track the performance of Ec2 instances, Lambda functions, and other resources
- Troubleshooting
	Identify and resolve issues by analyzing logs and metrics
- Cost Optimization
	Monitor resource utilization to optimize costs
- Application performance Monitoring
	Track application performance and identify bottlenecks
### Common Use Cases
- Monitoring Ec2 Instance Health
	Track CPU utilization, memory usage, and disk I/O
- Monitoring Lambda function performance
	Track invocation errors, duration, and throttles
- Setting alarms for critical metrics
	Receive notifications when important metrics exceed thresholds
- Visualizing application performance
	Create custom dashboards to track key performance indicators (KPIs)

# Amazon Route 53 Resolver
- Amazon Route 53 Resolver is a DNS query resolution service provided by AWS. It allows you to resolve domain name system (DNS) queries across AWS, the internet, and on-premises networks
### How it Works
- Resolves DNS queries
	Route 53 Resolver can answer DNS queries for both public and private domains
- Hybrid Cloud Support
	It enables seamless DNS resolution between AWS and on-premises environments
- Custom Routing
	You can configure custom routing rules to control how DNS queries are resolved
- Security
	It offers features like DNS firewall to protect against DNS-based attacks
### Key benefits
- Improved Performance: Reduces DNS query latency
- Enhanced Security: Protects against DNS threats
- Simplified Management: Centralized Management of DNS resolution across environments
- Cost-Effective: Optimized for performance and Cost-efficiency
### Common Use Cases
- resolving DNS queries for Ec2 instances within a VPC
- Forwarding DNS queries to on-premises DNS servers
- Protecting against DNS-based attacks with DNS Firewall
- Improving application performance with faster DNS resolution
### In Use
- An application is running on an Amazon EC2 instance in a VPC with the default DHCP option set. The application connects to an on-premises Microsoft SQL
- Server database with the DNS name mssql.example.com. The application is unable to resolve the database DNS name
	- **Create an Amazon Route 53 Resolver outbound endpoint. Add a forwarding rule for the domain example.com. Associate the forwarding rule with the VPC**
	Inbound endpoints are used to forward DNS queries from your network to Route 53 Resolver within your VPC. They specify the IP addresses that DNS resolvers on your network should forward DNS queries to. This is the opposite of what the scenario requires
	The Scenario involves resolving DNS queries originating from an Amazon EC2 instance within a VPC. Therefore, the correct approach is to configure outbound forwarding, not inbound forwarding
	This answer correctly describes the solution by suggesting the creation of an outbound endpoint and adding a forward rule for the domain example.com to forward DNS queries from the VPC to DNS resolver on the network
# VPC Peering Connection
- A VPC peering connection is a networking connection between two VPCs that enables you to route traffic between them using private IPv4 or IPv6 addresses
- Essentially it allows instances in one VPC to communicate with instances in another VPC as if they were on the same network
#### Key Points
- Private Connection
	Traffic between peered VPCs never traverses the public internet
- Flexible
	Can be established between VPCs in the same or different AWS accounts and regions
- No Additional hardware
	Uses existing VPC infrastructure without requiring gateways or VPN connections
- Security
	Provides a secure way to connect VPCs without exposing resources to the public internet
#### Use Cases
- Connecting Different Environments
	Development, testing, and production environments can communicate securely
- Sharing Resources
	Share resources like databases or storage between VPCs
- Cost Optimization
	Reduce costs by moving workloads between VPCs based on availability or pricing
- Disaster Recovery
	Create a secondary region with a peered VPC for failover

# Routing Policies
- A routing policy is a set of riles that dictate how network traffic is forwarded through a network.
- It provides granular control over how data packets are routed, allowing network administrators to optimize network performance, security, and reliability
### How Routing Policies Work
Routing policies typically consist of conditions and actions
- Conditions
	There are criteria used to match incoming traffic. This can include source and destination IP addresses, protocols, ports, and other attributes
- Actions
	These are the actions taken when the conditions are met. this can include redirecting traffic to a specific interface, applying traffic shaping or marking traffic for QoS

### Types of Routing policies
- Import Policies
	Control which routes are imported into the routing table from external sources
- Export Policies
	Determine which routes are advertised to other network devices
- Policy-based routing (PBR)
	Allows traffic to be forwarded based on criteria other than the destination IP address

### Common Use Case
- Load Balancing: Distribute traffic across multiple servers
- Traffic Engineering: Optimize network performance by controlling traffic flow
- Security: Filter traffic based on security policies
- Quality of Service (QoS): prioritize critical traffic over less important traffic
- Network address translation (NAT): Translate private IP addresses to public IP addresses
### In Use
- A company expanded its webs application to serve a worldwide audience. A SysOps administrator has implemented a multi-region AWS deployment for all production infrastructure. The SysOps administrator must route traffic based on the location of resources
- Which Amazon Route 53 routing policy should the SysOps admin use
	- **Geoproximity Routing Policy**
	- This is the answer because the question states that "base on location of resources". geolocation is used for based on location of users
	- This policy is useful when you want to provide different responses or direct traffic to specific resources based on the user's location


# AWS Budgets
- AWS Budgets is a cost management tool that helps you set custom budgets for your AWS usage and receive alerts when those budgets are exceeded or forecasted to be exceeded. Its a proactive way to monitor your AWS spending and avoid unexpected costs

### Key Features
- Custom Budgets
	Set budgets based on specific services, regions, or cost categories
-  Alers
	Receive notifications via email or SNS when budget thresholds are reached
- Forecasting
	Estimate future costs based on historical usage
- Actions
	Automate actions when budget threshold are exceeded, such as suspending IAM users or sending custom notifications
### Benefits
- Cost Control
	Prevent unexpected overspending by setting and monitoring budgets
- Improved Financial management
	Gain visibility into AWS spending and optimize costs
- Proactive Alerts
	Receive timely notifications of potential cost overruns
- Automation
	Automate cost management actions based on budget thresholds
### In Use
- A company needs to ensure struct adherence to a budget for 25 applications deployed on AWS. Separate teams are responsible for storage, compute, and database costs. A SysOps admin must implement an automated solution to alert each team when their projected spend will exceed a quarterly amount that has been set by the finance department. The solution cannot incur additional compute, storage, or database costs
	- **Use AWS Budgets to create a cost budget for each team, filtering by the services they own. Specify the budget amount defined by the finance department along with a forecasted cost threshold. Enter the appropriate email recipients for each budget**
	Budgets do not guarantee to stop you from exceeding a spend. There can be a delay between when you incur a charge and when you receive a notification from AWS budgets for the charge. This is due to a delay between when an AWS resource is used and when that resource usage is billed. You might incur additional costs or usage that exceeds your budget notification threshold before AWS Budgets can notify you. 

When you see that InstanceLimitExceeded is the error returned and you want to add an instance to mitigate traffic then you need to use a Service Quota to request an EC2 quota increase
	If it says [ Instance Limit Exceeded ] -> Over 64 vCPU
	If it says [ Insufficient Instance Capacity ] -> AWS's Problem
	If it says [ Instance Terminates Immediately ] -> EBS volume limit, or corrupt or no permission for decryption

When the application team doe not know the application's expected usage or expected growth then the SysOps Admin should recommend [ Creating a CloudWatch alarm that are based on anomaly detection ]

To reduce evictions when using an Amazon ElastiCache for Memcached Cluster you should Increase the individual node size inside the ElasticCache cluster and add an additional node to the ElasticCache cluster
[ Eviction occurs when the cache is full and a new item needs to be added, resulting in the removal of an existing item from the cache ]

# Ervin Szilagyi Notes
# IAM: Identity Access & Management 
- An **IAM user** account as an entity that represents a person or a service
- An **IAM policy** is a document that defines the permissions which are applied to users, groups and roles
	- Inline policies: policies which can be attached directly to the user
- **IAM Groups** are a collective of users which have the same policies applied to them. Policies applied to the group are inherently applied to the users which are par of the group. This makes easier to manage and apply policies for multiple users
- An **IAM Role** is an identity that can be assumed by a service
## Authentication Methods
- Access Keys:
	- Consists of an Access key ID and a secret key
	- User for programmatic access to the API
- IAM User accounts and passwords:
	- Used for authenticating to the AWS management Console

# Virtual Private Cloud (VPC) Core Concepts
- VPC is a logically isolated portion of the AWS cloud within a region
- Subnets are networks within a VPC. Subnets are created inside of an Availability Zone (AZ)
- Subnets can be public or private. Instanced in public subnet have their in public IP address
- Route Table:
	- Solve data routing within within a VPC or between a VPC and outside world
	- We can multiple route tables per VPC, each of them assigned to a subnet
- Internet Gateway: used to connect with the outside world
	- 0.0.0.0/0 address is added to the route table, all traffic which does not have a private destination is routed through the internet gateway
- We can have multiple VPCs in a region
- Each VPC has a CIDR block assigned (Example `10.0.0.0/16`)
	- **a CIDR block is a collection of IP addresses that share the same network prefix and number of bits**
- Default VPC: by default an AWS account has a VPC created in each region
- For the default VPC we get a default subnet created in each AZ for each location (can be between 2 and 6 subnets)
- For the default subnets we get a default internet gateway -> each default subnet is basically public
## Public and Private Services
- Public services have a public IP address, they can be reached from the internet
- Everything launched in a VPC gets a private IP address
- Private services don't have a public IP
- Private instances can connect to the internet through a NAT instance
- Private instances can also access other AWS services using a VPC end-point

# Deployment Automation - Elastic Beanstalk
- Elastic Beanstalk is a developer centric view of deploying an application on AWS
- It is free, but we pay for the underlying hardware
- It is managed service and it will provide:
	- An Instance configuration / OS is handled by Beanstalk
	- A deployment strategy which is configurable
- Beanstalk offers 3 architecture modes:
	- Single instance deployment: great for development