#### VPC Primer
- VPC, Subnets, Internet Gateways & NAT Gateways
- Security Groups, Network ACLs (NACL), VPC Flow Logs
- VPC Peering, VPC Endpoints
- Site to Site VPN & Direct Connect

### VPC & Subnet Primer
- VPC 
	- Private network to deploy your resources (regional Resources)
- Subnets 
	- Allow you to partition your network inside your VPC (Availability Zone Resource)
- A **public subnet** is a subnet that is accessible from the internet
- a **private subnet** is a subnet that is not accessible from the internet
- To define access to the internet and between subnets, we use **Route Tables**

### Internet Gateway & NAT Gateway
- **Internet Gateway** helps our VPC Instances connect with the internet
- Public Subnets have a route to the internet gateway

- **NAT gateway**(AWS-managed) & **NAT Instance** (Self-managed) allow your instances in your **Private Subnets** to access the internet while remaining private

NAT Gateways are usually associated with the Private Subnets and Internet Gateways are associated with Public Subnets.
But the NAT gateway connects to the Internet Gateway

### Network ACL & Security Groups
- NACL (Network ACL)
	A firewall which controls traffic from and to subnet
	Can have ALLOW and DENY rules
	Are attached at the **Subnet** level 
	Rules only include IP addresses
	**At the Subnet Level**
	
- Security Groups
	A firewall that controls traffic to and from an ENI (Elastic Network Interface) / an EC2 Instance
	Can only have ALLOW rules
	Rules include IP addresses and other security groups

Default NACL lets everything in and everything out

| **Security Group**                                                                                                                                              | **Network ACL**                                                                                                                                      |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| Operates at the Instance Level                                                                                                                                  | Operates at the subnet level                                                                                                                         |
| Supports allow rules only                                                                                                                                       | Supports allow rules and deny rules                                                                                                                  |
| Is stateful: Return traffic is automatically allowed, regardless of any rules                                                                                   | Is stateless: Return traffic must be <br>explicitly allowed by rules                                                                                 |
| We evaluate all rules before deciding whether to allow traffic                                                                                                  | We process rules in number order when deciding whether to allow traffic                                                                              |
| Applies to an instance only if someone specifies the security group when launching the instance, or associates the security group with the instance<br>later on | Automatically applies to all instances in the subnets it's associated with (therefore, you don't have to rely on users to pecify the security group) |
#### VPC Flow Logs
- Captures information about IP traffic going into your interfaces:
	VPC Flow Logs
	Subnet Flow Logs
	Elastic Network Interface Flow Logs
- Helps monitor & Troubleshoot connectivity issues. Examples:
	Subnet to internet
	Subnet to Subnet
	Internet to Subnet
- Captures network information from AWS managed interfaces too: Elastic Load Balancers, ElastiCache
- VPC Flow Logs data can go to S3, CloudWatch Logs, and Kinesis Data Firehose

#### VPC Peering
- Connects two VPC, privately using AWS' Network
- Make them behave as if they were in the same network
- Must not have overlapping CIDR (IP address range)
	if the network ranges overlap then the network doesn't know where to go. So to connect two VPC, you need to make sure that the IP addresses range it operates on are different and not overlapping.
- VPC Peering connection is not transitive (must be established for each VPC that need to communicate with one another)
	You would need a Transit Gateway which allows multiple VPC's to connect to a hub for all of them to communicate in between.
- 