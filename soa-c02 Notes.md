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
	Without the appropriate route table updates, the EC2 instance in the private subnet will be able to communicate with the S3 bucket, even if the instance has the necessary S3 permissions. **

