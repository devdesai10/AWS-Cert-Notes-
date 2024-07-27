#### A SysOps administrator wants to manage a webserver application with AWS Elastic Beanstalk. The Elastic Beanstalk service must maintain full capacity for new deployments at all times 
- (**Option B**) Immutable (**Immutable deployment performs an immutable update to launch a full set of new instances running the new version of the application in a separate Auto Scaling group, alongside the instances running the old version. immutable deployments can prevent issues caused by partially completed rolling deployments. if the new instances don't pass the health checks, Elastic Beanstalk terminates them, leaving the original instances untouched**)
- (**Option E**) Rolling with additional batch (**To maintain full capacity during deployments, you can configure your environment to launch a new batch of instances before taking any instances out of service. This option is known as a rolling deployment with an additional batch. When the deployment completes, Elastic Beanstalk terminates the additional batch of instances**)

#### A SysOps administrator wants to monitor the free disk space that is available on a set of Amazon EC2 Instance that have Amazon Elastic Block store (Amazon EBS) volumes attached. The SysOps administrator wants to receive a notification when the used disk space of the EBS volumes exceeds a threshold value, but only when the DiskReadOps metric also exceeds a threshold value. The SysOps administrator has set up an Amazon Simple Notification Service (Amazon SNS) topic. How can the SysOp Admin receive notification only when both metrics exceed their threshold values?
- Install the Amazon CloudWatch agent on the EC2 Instances. Create a metric alarm for the disk space and a metric alarm for the DiskReadOps metric. Create a composite alarm that includes the two metric alarms to publish a notification to the SNS topic (**EBS Volume Exceeded and DiskReadOps Exceeded usually means you have to create a composite alarm, You also have to install the CloudWatch Agent because you dont have disk usage metrics by default**)

#### A company with multiple AWS accounts needs to obtain recommendations for AWS Lambda functions and identify optimal resource configurations for each Lambda function
- Enable AWS Compute Optimizer and export the Lambda function recommendations (**optimal usually look for optimizer**)

#### A company must ensure that any objects uploaded to an S3 bucket are encrypted
- (**Option C**) Implement Amazon S3 default encryption to make sure that any object being uploaded is encrypted before it is stored 
- (**Option E**) Implement S3 bucket policies to deny unencrypted objects from being uploaded to the buckets

#### A SysOps administrator is using AWS Systems Manager Patch Manager to patch a fleet of Amazon Ec2 instances. The SysOps administrator has configured a patch baseline and a maintenance window. The SysOps administrator also has used an instance tag to identify which instances to patch. 
#### The SysOps Administrator must give Systems Manager the ability to access the EC2 Instances
- Attach an IAM instance profile with access to Systems Manager to the instances (**By default, AWS Systems Manager doesn't have permission to perform actions on your instances. Grant access by using an AWS Identity and Access Management (IAM) instance profile. An instance profile is a container that passes IAM role information to an Amazon Elastic Compute Cloud (Amazon EC2) instance at launch. You can create an instance profile for Systems Manager by attaching one or more IAM policies that define the necessary permissions to a new role or to a role you already created.**)

#### An AWS CloudFormation template creates an Amazon RDS instance. This template is used to build up development environments as needed and then delete the stack when the environment is no longer required. The RDS-persisted data must be retained for further use, even after CloudFormation stack is deleted.
- Use the Snapshot Deletion Policy in the CloudFormation template definition of the RDS instance. (**Since you are trying to delete resoource but keep a backup. retain will keep the instance itself**)

#### A SysOps administrator configures VPC flow logs to publish Amazon CloudWatch Logs. The SysOps administrator reviews the logs in CloudWatch Logs and notices less traffic than expected. After the SysOps admin compares the VPC flow logs to logs that were captured on premises, the SysOps Admin believes that the flow logs are incomplete
- VPC flow logs cannot capture traffic from on-premises servers to VPC (**VPC Flow Logs is a feature that enables you to capture information about the IP traffic going to and from network interfaces in your VPC**)

#### A company is managing a website with a global user base hosted on Amazon EC2 with an Application load Balancer (ALB). To reduce the load on the web servers, a SysOps admin configures an Amazon CloudFront distribution with the ALB as the origin. After a week of monitoring the solution, the administrator notices that requests are still being served by the ALB and there is no change in the web server load. 
- (**Option D**) The default, minimum, and maximum Time to Live (TTL) are set to 0 seconds on the CloudFront distribution. (**If the Time to Live (TTL) settings are set to 0 seconds, it means that CloudFront will not cache any responses from the ALB and will forward each request directly to the ALB. This will result in the ALB still serving all the requests, and there won't be any offloading of the web server load**)
- (**Option B**) The DNS is still pointing to the ALB instead of the CloudFront distribution (**If the DNS is still directing user traffic directly to the ALB instead of the CloudFront distribution, then the requests will not be served through CloudFront, and there won't be any reduction in the web server load.**)

#### A SysOps Administrator is testing an application that is hosted on five Amazon EC2 instances. The instances run in an Auto Scaling group behind an Application Load balancer (ALB). High CPU utilization during load testing is causing the Auto Scaling group to scale out. The SysOps administrator must troubleshoot to find the root cause of the high CPU utilization before the Auto Scaling Group scales out. 
- Suspend the Launch and Terminate process types (**The goal is to find the root cause of the high CPU util meaning we need to suspend the scaling events**)

#### A company is attempting to manage its cost in the AWS Cloud. A SysOps admin needs specific company-defined tags that are assigned to resources to appear on the billing report. 
- Activate the tags as user-defined cost allocation tags (**Use Billing serves to activate the user defined cost. This is told when the SysOps admin needs the company-defined tags that are assigned to resources**)

#### A Company has an internal web application that runs on EC2 instances behind an ALB. The instances run in an Auto Scaling Group in a single AZ. A SysOps admin must make the application highly available.
- Update the Auto Scaling Group to launch new instances in a second AZ in the same AWS Regions (**Auto Scaling for high availability would be to create it in a second AZ**)

#### A SysOps admin is troubleshooting an AWS CloudFormation template whereby multiple Amazon EC2 instances are being created. The template is working in us-east-1, but it is failing in us-west-2 with the error code `AMI [ami-12345678] does not exist` How should the admin ensure that the AWS CloudFormation template is working in every region?
- Modify the AWS CloudFormation template by including the AMI IDs in the :Mappings: section. Refer to the proper mapping within the template for the proper AMI ID

#### A company has a policy that requires all Amazon EC2 instances to have a specific set of tags. If an EC2 instance does not have the required tags, the noncompliant instance should be terminated. What is the MOST operationally efficient solution
- Create a AWS Config rule to check if the required tags are present. If an EC2 Instance is noncompliant, invoke an AWS Systems Manager Automation document to terminate the instance.

#### A company has an Auto scaling group of Ec2 instances that scale based on average CPU utilization. The Auto scaling group events log indicates an `InsufficientInstanceCapacity error` Which action should the SysOps Admin take to remediate this issue?
- Change the instance type that the company is using
- Configure the Auto Scaling Group in different Availability Zones

#### A SysOps admin needs to control access to groups of Amazon Ec2 instances using AWS Systems Manager Session Manager. Specific tags on the EC2 instances have already been added. 
- Attach and IAM policy to the user or groups that require access to the Ec2 Instances (**IAM policies can be used to control access to resources in AWS. The policy can specify which actions are allowed or denied and which resources the user or group can access. In this case, the policy should include permissions to use the Session Manager service**)
- Create an IAM policy that grants access to any EC2 instances with a tag specified in the condition element (**This policy can specify that access is granted only to instances with specific tags. For example, a policy could specify that users or groups can only access instances that have a specific tag, such as "Environment=Prod". This helps to ensure that only the appropriate instances are accessed**)

#### A company has an AWS Lambda function in Account A. The Lambda function needs to read the objects in an Amazon S3 bucket in Account B. A SysOps administrator must create corresponding IAM roles in both accounts. 
- In Account A, create a Lambda execution role to assume the role in Account B. Create a role that the function can assume to gain access to the S3 bucket. 

#### An AWS Lambda function is intermittently failing several times a day. A SysOps Admin must find out how often this error has occurred in the last 7 days.
- Use Amazon CloudWatch Logs Insights to query the associated Lambda function logs 

#### A company is using Amazon CloudFront to serve static content for its web application to its users. The CloudFront distribution uses an existing on-premises website as a custom origin.
#### The company requires the use of TLS between CloudFront and the origin server. This configuration has worked as expected for several months. However, users are now experiencing HTTP 502 (Bad Gateway) errors when they view webpages that include content from the CloudFront distribution.
- Examine the expiration date on the certificate on the origin site. Validate that the certificate has not expired. Replace the certificate if necessary. 

#### An Amazon CloudFront distribution has a single Amazon S3 bucket as its origin. A SysOps admin must ensure that users can access the S3 bucket only through requests from the CloudFront endpoint
- Create an Origin Access Identity (OAI). Assign the OAI to the CloudFront distribution. Update the S3 bucket policy 

#### A company uploaded its website files to an Amazon S3 bucket that has S3 versioning enabled. The company uses an Amazon CloudFront distribution with the S3 bucket as the origin. The company recently modified the files, but the object names remained the same. users report that old content is still appearing on the website. 
- Create a CloudFront invalidation, and add the path of the updated files. **By default, CloudFront caches a response from Amazon S3 for 24 hours (Default TTL of 86,400 seconds) If your request lands at an edge location that served the Amazon S3 response within 24 hours, then CloudFront uses the cached response. This happens even if you updated the content in Amazon S3**

#### A company host a static website on Amazon S3. An Amazon CloudFront distribution presents this site to global users. The company uses the Managed- 
#### CachingDisabled CloudFront cache policy. the company's developers confirm that they frequently update a file in Amazon S3 with new information
#### Users report that the website presents correct information when the website first loads the file. However, the users' browsers do not retrieve the updated file after a refresh.
- Add a Cache-Control header field with max-age=0 to the S3 object **You can control how long your files stay in a CloudFront cache before CloudFront forwards another request to your origin. Reducing the duration allows you to serve dynamic content. Increasing the duration means that your users get better performance because your files are more likely to be served directly from the edge cache. A longer duration also reduces the load on your origin.**

