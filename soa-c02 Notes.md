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

# [Ervin Szilagyi Notes](https://ervinszilagyi.dev/certified-aws-sysops-associate/)
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

# EC2 
## Placement Groups
- Sometimes we want control over the EC2 instance placement strategy
- This strategy can be defined using placement groups
- When we create a placement group, we specify one the following strategies:
	- **Cluster**: places instances into a low latency group in a single AZ
	- **Spread**: spreads instances across underlying hardware (limitation: max 7 instances per group per AZ)
	- **Partition**: similar to spread, instances are spread across many different partitions (different sets of racks) within an AZ. Can scale up to hundreds of EC2 instances per group. Recommended for Hadoop, Cassandra, Kafka
## Cluster Placement Group
- All instances are placed on the same rack, same AZ
- Pros: great network (10Gbps bandwidth between instances)
- Cons: if the rack fails, all instances fail at the same time
- **Use Cases**:
	- Big Data jobs that needs to complete fast
	- Application that needs extremely low latency and high network throughput
## Spread Placement Group
- All the Ec2 instances are located on different hardware
- Pros:
	- Can span across AZs
	- Reduced risk for simultaneous failure
- Cons:
	- Limited to 7 Instances per AZ per placement group
- **Use Cases**:
	- Application that needs to maximize high availability
	- 
	- Critical applications where each instance must be isolated from failure from each other
## Partition Placement Group
- Partitions are sets of racks
- We can create up to 7 partitions in case of partition placement group
- We can have hundreds of EC2 instances as part of a placement group
- The instances in a partition do not share racks with the instances in the other partitions
- A partition failure can affect many EC2 instances but won't affect other partitions 
- EC2 instance get access to the partition information as metadata
- Use Cases:
	- HDFS
	- HBase
	- Cassandra
	- Kafka
## Shutdown Behavior
- Shutdown Behavior: how should an instance react when shutdown is done using the OS?
	- Stopped: default
	- Terminated 
- Shutdown Behavior is not applicable from AWS Console or AWS API, it applies to shutdowns from inside the VM
- CLI Attribute: `InstanceInitiatedShutdownBehavior`
- Termination protection: protects against accidental termination in AWS Console or CLI
- We have instance where shutdown behavior is "terminate" and termination in AWS Console or CLI
- We have an instance where shutdown behavior is "terminate" and termination protection is enabled. When we shutdown the instance from the OS, the instance still be terminated
## EC2 Launch Troubleshooting
- #InstanceLimitExceeded error: means that we have reached the limit of max number of instances per region (As of September 019, this limit is counted in vCPU instead of instances, default is 32)
	- Solution: launch the instance in a different region or create a support ticket to increase the limit. Default time is: 20
- #InsufficientInstnaceCapacity : It means AWS does not have that much On-Demand capacity in the particular AZ in order for the instance to be launched 
	- Solutions:
		- Wait for a few minutes before requesting again
		- If more than once instance is requested, we can break down the request by creating the instance one by one
		- If urgent submit a request for a different instance type and upgrade it afterwards
- #InstanceTerminateImmediately (The instance goes from the pending state to the terminated state)
	- EBS volume limit is reached
	- EBS snapshot is corrupt
	- The root EBS volume is encrypted and we don't have permission to access the KMS key for decryption
	- The instance store-backed AMI that we are using to launch the instance is missing a required part (an image.part.xxx file)
- **To find the exact reasons: check the EC2 console of AWS - Instances - Description tab - State transition reason**
## EC2 SSH Troubleshooting
- We have to make sure the private key (pem file) has 400 permissions, else we get
	- *Unprotected Private Key File Error*
- We have to make sure the username for the OS is given correctly when logging via SSH, else we get a "Host key not found" error 
- Connection timeout reasons:
	- SG is not configured correctly
	- CPU load of the instance is high
# EC2 Instance Launch Types
- On Demand Instances: short workload, predictable pricing
- Reserved (minimum 1 year)
	- Reserved Instances: long workloads
	- Convertible Reserved Instances: long workload with flexibility instance types
	- Scheduled Reserved Instances

- Spot Instances: Short Workloads for cheap. Instance can be lost over time
- Dedicated Instances: no other customers will share the hardware
- Dedicated Hosts: book an entire physical server, we can control instance placement
### EC2 On Demand
- Pay for what we use
- Billing is happening per second after the first minute
- Has the highest cost but does not require any upfront commitment
- Reservation period can be 1 or 3 years
- We can reserve a specific instance type
- Recommended for steady state usage application (Example: database)
### EC2 Reserved Instances
- Up to 75% discount compared to On-Demand
- Pay upfront for what we use with long term commitment
- Reservation period can be 1 or 3 years
- We can reserved a specific instance type
- Recommended for steady state usage applications (Example: database)
### Convertible Reserved Instances
- Similar as Reserved Instances
- We can change the EC2 instance type
- Up to 54% discount
### Scheduled Reserved Instances
- Instances which are reserved and are launched within a time window
- Recommended when we require compute for a fraction of the day, week, month
### Dedicated Hosts
- Physical dedicated EC2 server for our use
- Offers full control of EC2 instance placements
- Offers visibility into the underlying sockets/physical cores of the hardware
- Can be allocated for 3 years period reservation
- More expensive
- Useful for software that have complicated licensing model (BYOL - Bring Your Own License) or string regulatory compliance needs
### Dedicated Instances
- Instances are running on hardware dedicated for the account
- May Share hardware with other instances from the same account
- We have no control over instance placement (can move hardware after Stop/Start)
### EC2 Spot Instances
- Can get a discount of up to 90% compared to On Demand Instances
- We can define a max spot price and get the instance of our price is bigger than the current price
- If the current spot price goes beyond our max price, we can choose to stop or terminate the instance within 2 minutes grace period
- If we don't want our spot instance to be reclaimed by AWS, we can use a **Spot Block**
	- We can block a spot instance during a specified time frame (1 to 6 hours) without interruptions
	- In rare situations the instance may be reclaimed

- Use cases for spot instances: batch jobs or workloads that are resilient to failure
- We can launch spot instances with a spot request. A spot request contains the following information:
	- Maximum Price
	- Desired number of instances
	- Launch Specification
	- Request type: on-time, persistent
	- Valid from, valid until

- Request types:
	- One time request: as soon as the request is fulfilled, the request will go away
	- Persistent request: the number of instances is attempted to be kept even if some instances are reclaimed, meaning that the request will not go away as soon as it is completed first time

- Canceling a spot instances: in order to cancel a spot instance, it has to be in an **open, active** or **disabled** state
- Canceling a spot request, it will not terminate the instances themselves. In order to terminate instances, first we have to terminate the spot request, if there is one active
### Spot Fleets
- Spot Fleet - set of spot instances + (optional) on-demand instances
- The spot fleet will try to meet the target capacity with price constraints
- A launch pool can have the following can have different instance types, OS, AZ
- We can have multiple launch pools, so the fleet can choose the best
- Spot fleet will stop launching instances the target capacity is reached
- Strategies to allocate spot instances:
	- **lowestPrice**: The spot fleet will launch instances from the pool with the lowest price
	- **diversified**: distribute instances across all pools
	- **capacityOptimized**: launch instances based on the optimal capacity for the number of instances

- Spot Fleets allow us to automatically request spot instances with the lowest price
## EC2 Instances Types
- R: applications that need a lot of RAM, example in-memory caches
- C: applications that need a good CPU, example compute/databases
- M: applications that are balanced, example general web-app
- I: applications that need a good local I/O (instance storage), example databases
- G: applications that need a GPU, example video-rendering, ML
- T2/T3: burstable instances
- T2/T3 - unlimited: unlimited CPU burst, we get charged for burst
### Burstable Instances (T2/T3)
- Burst: when a machine needs to process something unexpected (a spike), it can burst the CPU power
- If the machine bursts, it will utilize burst credits
- If the credits are gone, the machine CPU performance will suffer
- If the machine is stopped, burst credits do accumulate over time 
- The bigger the instance, the faster we can earn back burst credits
- T2/T3 unlimited: offer unlimited burst credit balance. If the instance used all its burst credits, we pay extra for the additional bursts
### AMI
- Virtual machine images with customized set-up/software
- Custom AMI can provide the following advantage
	- Pre-install packages
	- Faster boot time (no need to configure user data)
	- Machine come pre-configured with monitoring 
	- Security concerns - control over the machine in the network
	- Control of maintenance and updates of AMI over time
	- Active Directory Integration out of the box
	- Installing out app ahead of time
	- Using someone's AMI which is optimized for running an app (example: database)
- AMIs are not global, they are built for a specific region
### Using Public AMIs
- We can leverage AMIs from other people
- We can pay for other people's AMI by the hour
- AMIs can be found and published on the Amazon Marketplace
### AMI Storage 
- AMI take space and they live in Amazon S3
- By default AMIs are private and locked for the account who created it
- We can make AMIs public and share them with other AWS accounts or sell them on the AMI marketplace
### AMI Pricing
- AMI take space and they live in Amazon S3
- Overall it is quite inexpensive to store private AMIs
- We have to make sure to remove AMIs we don't use to save costs
### Cross account AMI Copy
- It is possible to share AMI with another AWS account
- Sharing an AMI does not affect the ownership of the AMI
- if a shared AMI is copied, than the account who did the copy becomes the owner
- To copy an AMI that was shared from another account, the owner of the source AMI must grant read permissions for the storage that backs the AMI, either the associated EBS snapshot or an associated S3 bucket
- Limits:
	- An encrypted AMI can not be copied. Instead, if the underlying snapshot and encryption key where shared, we can copy the snapshot while re-encrypting it with a key of our own. The copied snapshot can be registered as a new AMI
	- We cant copy an AMI with an associated **billingProduct** code that was shared with us from another account. This includes Windows AMIs and AMIs from the AWS Marketplace. To copy a shared AMI with **billingProduct** code, we have to launch an Ec2 instance from our account using the shared AMI and then create an AMI from source
# Elastic IPs
- when we stop and then start an EC2 instance, the public IP will change
- If we need to have a fixed public IP, we need an Elastic IP
- An Elastic IP is a public IPv4 Ip we own as long as we don't delete it
- An Elastic IP can be attached to one instance at a time
- We can remap it across instances
- We don't pay for the Elastic IP if it is attached to a VM
- With an Elastic IP we can mask the failure of an instance or software by rapidly remapping the address to another instance in our account
- We can have up to 5 Elastic IPs in an account (soft limit, can be requested to be increased)
- Overall try we should try to avoid using Elastic IPs:
	- We could use a random public IP and register a DNS name to the instance
	- Use a Load Balancer with a static hostname
# CloudWatch Metrics for EC2
### AWS Provided Metrics
- Basic Monitoring (default): metrics are collected at a 5 minute interval
- Detailed Monitoring (paid): metrics are collected at a 1 minute interval
- AWS provided Metrics include: CPU, Network, Disk and Status Check metrics
### Custom Metrics
- Basic Resolution of custom metrics is 1 minute
- High Resolution can go all the way up to 1 second
- Custom metrics can include RAM, application level metrics
- IAM permission is required on the EC2 instance role to be able to push metrics to CloudWatch
## EC2 Included Metrics
- CPU: CPU Utilization + Cred Usage / Balance (in case of T2/T3)
- Network: Network In/Out
- Status  Checks:
	- Instance Status: Checks for the EC2 VM
	- System Status: checks for the underlying hardware (amazon health checks, no user control is granted over them)
- Disk (only for instance stored based instances): Read/Write for Ops/Bytes
- **RAM is NOT included in AWS EC2 metrics!**
## CloudWatch Unified Agent
- new kind of metrics, gather logs and metric at the same time
# SSM - AWS Systems Manager
- SSM helps manage EC2 and On-Premise Systems at scale
- Offers Operation insights about the state of the infrastructure
- Problems can be easily detected with it
- Offers patching automation for enhanced compliance
- Works on both Windows and Linux
- Integrates with CloudWatch metrics and dashboards
- Integrates with AWS Config
- It is a free service
## SSM Features
- Resource Groups
- Insights
	- Insights Dashboard
	- Inventory: discover and audit the software installed
	- Compliance
- Parameter Store
- Actions:
	- Automation (shutdown EC2 instances, create AMIs)
	- Run Command
	- Session Manager
	- Maintenance Windows
	- State Manager: define and maintaining configuration of OS and applications
## How Systems Manager Works
- Instances need to install the SSM agent
- This is installed by default on Amazon Linux AMI and on some Ubuntu AMIs
## AWS Tags
- We can add text key-value pairs called tags to many AWS Resources
- Tags have free naming conventions, common tags are: Name, Environment, Team, Etc.
- They are used for:
	- Resource Grouping
	- Automation
	- Cost Allocation
## AWS Resource Groups
- We can create, view or manage logical group of resources using tags
- AWS Resource Groups allow creation of logical groups of resource such as:
	- Applications
	- Different Layers of an application stack
	- Production/development environments
- AWS Resource Groups is a regional service
## SSM Documents
- Documents can be in JSON or YAML
-  We can define parameters, actions
## SSM Run Command
- Execute a document or just run a command
- This can be done across multiple instances using resource groups
- There is a possibility to have rate control / error control 
- It is integrated with IAM and CloudTrail 
## Using SSM to Patch Instances
- Inventory: list software on an Instance
- Inventory + Run Command: Patch software
- Patch Manager + maintenance Window: path OS
- Patch Manager: gives compliance
- State manager: ensures that instances are in a consistent state (compliance)
## AWS Systems Manager Session Manager
- Allows to start a secure shell on a VM
- **Does not use SSH access and bastion hosts**
- Only works for EC2 for now
- Log actions done through secure shells to S3 and CloudWatch
- IAM permissions: access SSM + write to s3 + write to CloudWatch
- CloudTrail can intercept StartSessions events
- AWS Secure Shell compared to SSH:
	- No need to open port 22 at all anymore
	- No need for a bastion host
	- All commands are logged to S3/CloudWatch
	- Access to secure Shell is done through User IAM, not SSH keys
## What if I lost my SSH key for EC2
- Traditional method: If the instance is EBS backed
	- We have to stop the instance and detach the root volume
	- Attach the root volume to another instance as a data volume
	- Modify the ~/.ssh/authorized_keys file with a new key
	- move the volume back to the stopped instance
	- Start the instance
- New Method: If the instance is EBS: 
	- Run the AWSSupport-ResetAccess automation document in SSM

## Common Reasons for Stack operation Failure
**Problem: A stack operation failed, and the stack instance status is OUTDATED**
	Cause: There can be several common causes for stack operation failure
	The template could be trying to create global resources that must be unique but aren't, such as S3 buckets
If the CloudFormation wants to create a new S3 bucket with a name but this name is always in use by another S3 bucket. 

## Increase in traffic caused read request to be throttled 
Create an Amazon CloudWatch alarm that use the ConsumedReadCapacityUnits metric. set the alarm threshold to a value that is close tot he DynamoDB table's provisioned capacity. Configure the alarm to publish notifications to the SNS topic
**By setting up these CloudWatch alarms and configuring them to send notifications to the SNS topic, the operations team will receive alerts before the Dynamo DB table starts throttling read requests. This will give them enough time to take appropriate actions, such as increasing the provisioned read capacity or investigating the root cause of the increased traffic**

## Windows file shares for users on premises with minimum latency
- Amazon FSx File Gateway 
	- To meet the requirements of presenting user file shares on premises and making the file shares available on AWS with minimum latency the sysops admin should set up a Amazon FSx File Gateway 

## Backups with Requirements
Use AWS Backups
- has to be AWS Backup if EBS Snapshot is not mentioned in the requirements
- Data LifeCycle Manager is for when you want to automate the creation, retention, and deletion of EBS snapshots
- AWS Backups to manage and monitor backups across the AWS Services you use, including EBS volumes, from a single place

## The company's security administrator has their own AWS account and wants to review the VPC configuration of developer AWS accounts
- Create an IAM policy in each developer account that has read-only access related to VPC resources. Assign the policy to a cross-account IAM role. Ask the security admin to assume the role from their account

## 403 Forbidden -Access Denied for a static website
- Add a bucket policy that grants everyone read access to the bucket objects
	- if an access denied error is returned by the web browser or curl command, then the object isn't publicly accessible. To allow public read access to your S3 object, create a bucket policy that allows public read access for all objects in the bucket

## SysOps admin needs to grant permissions for the application to access an Amazon DynamoDB table
- Create an IAM role to access the DynamoDB table. Assign the IAM role to the EC2 instance profile
	- From a security standpoint always try to prioritize using roles over users
	- Access to Amazon DynamoDB requires credentials. Those credentials must have permissions to access AWS resources, such as an amazon DynamoDb table or an Amazon Elastic Compute Cloud (Amazon EC2) instance. 

## Company updated 150 images on a website. The website is not displaying the images. What should the SysOps admin do to refresh the cache with the new images
-  Issue a CloudFront invalidation request to immediately expire the new images from the marketing team's update
	- To ensure that users receive the latest content, the cached content in CloudFront needs to be invalidated

## Company uses Amazon Route 53 for DNS on AWS, as well as having a on-premises server, The company wants the on-premises servers to use Route 53 for DNS resolution of the private hosted zone
- Create a Route 53 inbound endpoint. Ensure that security groups and routing allows the traffic from the on-premises data center. Configure the DNS server on the on-premises network to conditionally forward DNS queries for the private hosted zone's domain name to the IP addresses of the inbound endpoint
	- Inbound Resolver endpoints allow DNS queries to your VPC from your on-premises network or another VPC.
	- By creating a Route 53 outbound endpoint, the on-premises servers can forward DNS queries for the private hosted zone's domain name to Route 53. This allows the on-premises servers to resolve DNS queries for the private hosted zone's domain name to Route 53

## Custom Dimensions for data collection
- When given the question that you need custom dimensions than you use append_dimensions field in the CloudWatch agent 
- an example of CloudWatch agent config file 

  "append_dimensions" : {
  "ImageId" : "${aws:ImageId}"
  "InstanceId" : "${aws:InstanceId}"
  }

- In custom metrics, the --dimensions parameter is common. A dimension further clarifies what the metric is and what data it stores. You can have up to 30 dimensions assigned to one metric, and each dimension is defined by a name and value pair

## Regular backups available in another AWS region
- Modify the DB Instance. Enable Cross-Region Automated Backups 

## Users are reporting random logouts from the web application, what can be done to resolve it
- Configure cookie forwarding in the CloudFront distribution cache behavior
- Enable Sticky Sessions on the ALB target group

## CLI to deploy one of the sites certificates to the load balancer
- aws elb set-load-balancer-listener-ssl-certificate --load-balancer-name my-load-balancer --load-balancer-port 443 --ssl-certificate-id arn:aws:iam::12345689012:server-certificate/new-server-cert
	- Sets the certificate that terminates the specified listener's SSL connections. The specified certificate replaces any prior certificate that was used on the same load balancer and port
	- deploy certificate to "Load Balancer" -> aws elb

## Users not being able to connect to the specific EC2 instance using Sessions Manager
- Assign the AmazonSSMManagedInstanceCore managed policy to the EC2 instance profile for the Ubuntu Instance
	- To resolve the issue of users being unable to connect to the specific EC2 instance using Session manager, the SysOps administrator should assign the AmazonSSMManagedInstanceCore managed policy to the EC2 instance profile for the Ubuntu instance. this managed policy provides the necessary permissions for the SSM Agent to communicate with the Systems Manager service, which is required for Session manager to work. Once the policy is attached to the instance profile, users should be able to connect to the instance using Session Manager
## To delete unneeded data from the S3 bucket by using the CLI during a migration
- Assume a rile that has the s3:BypassGovernanceRetention permission
- Include the x-amz-bypass-governance-retention:true header in the request when issuing the delete command
To override or remove governance-mode retention settings, a user must have the s3:BypassGovernanceRetention permission and must explicitly include  x-amz-bypass-governance-retention:true as a request header with any request that requires overriding governance mode
- In governance mode, users can't overwrite or delete an object version or alter its lock settings unless they have special permissions. With governance mode, you protect objects against being deleted by most users, but you can still grant some suers permission to alter the retention settings or delete the object if necessary. You can also use governance mode to test retention-period settings before creating a compliance-mode retention period 

## When the CloudWatch Alarms are not in ALARM state 
- You have to reconfigure the CloudWatch alarms to use the VolumeReadBytes metric and the VolumeWriteBytes metric for the EBS Volume
CloudWatch can monitor I/O based on an entire EBS volume without the agent using the VolumeWriteBytes metric. The question is aksing about "volume metrics" if the question were asking about alerting for used or free space in a file system on a volume, the you'd need the CloudWatch agent running on the OS to analyze things from the OS perspective, including I/O with the DiskWriteBytes metric. The VolumeWriteBytes and DiskWriteBytes metrics are basically looking for the same thing. its like looking at a bucket from the inside or the outside to see what size it is. Both work. 
## Company created a CloudFront distribution in front of the application and would like www.example.com to access the application through CloudFront
- Create an ALIAS record in Amazon Route 53 that points to the CloudFront distribution URL
	- ALIAS records are a type of DNS record in Route 53 that allows you to map your domain name to AWS resources such as CloudFront distributions, S3 buckets, and more
	- Unlike CNAME records, ALIAS records do not incur additional DNS query charges
	- They can also be used at the root domain level, which is not possible with CNAME records
\
## VPC has public and private subnets. The company's security policy requires all EC2 instances to be deployed in private subnets
- Add a NAT gateway to public subnet. In the route table for the private subnets, add a route to the NAT gateway
	The application needs to be able to download updates from the internet, but it's running on EC2 instances in a private subnet. Private subnets do not have direct access to the internet. A NAT gateway allows instances in a private subnet to connect to the internet or other AWS services but prevent the internet from initiating a connection with those instances

## After adding and configuring the required components to the VPC, the admin is unable to connect to any of the domains that reside on the internet
- Rout ::/0 traffic to an egress-only internet gateway
	IPv4 = NAT instance/gateway | 0.0.0.0
	IPv6 = Egress-Only Internet Gateway | ::/0 
	**IPv6 addresses are globally unique, and are therefore public by default. If you want your instance to be able to access the internet, but you want to prevent resources on the internet from initiating communication with your instance, you can use an egress-only internet gateway. To do this, create an egress-only internet gateway in your VPC, and then add a route to your route table that points all IPv6 traffic (::/0) or a specific range of IPv6 address to the egress-only internet gateway. IPv6 traffic in the subnet that's associated with the route table is routed to the egress-only internet gateway**

## If after the release, penetration testing reveals a cross-site scripting vulnerability that could expose user data, What service will mitigate this issue
- AWS WAF

## 