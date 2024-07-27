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

# Amazon Machine Image