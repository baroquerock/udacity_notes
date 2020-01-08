# Cloud Computing

**Cloud Computing** is the delivery of IT resources over the Internet, the cloud is like a virtual data center accessible via the Internet

**Pay as you go** - you pay only for what you use and only when your code runs

**Autoscaling** - the number of active servers can grow or shrink based on demand

**Serverless** - allows you to write and deploy code without having to worry about the underlying infrastructure

_Benefits_:

- stop guessing about capacity
- avoid huge capital investments up front
- pay for only what you use
- scale globally in minutes
- deliver faster


## Types of Cloud Computing

**Infrastructure-as-a-Service (IaaS)** - the provider supplies virtual server instances, storage, and mechanisms for you to manage servers

**Platform-as-a-Service (PaaS)** - a platform of development tools hosted on a provider's infrastructure

**Software-as-a-Service (SaaS)** - a software application that runs over the Internet and is managed by the service provider


## Cloud Deployment Models

**Public Cloud** - a public cloud makes resources available over the Internet to the general public

**Private Cloud** - a private cloud is a proprietary network that supplies services to a limited number of people

**Hybrid Cloud** - a hybrid model contains a combination of both a public and a private cloud


## Logging In The Cloud

**Logging** provides visibility into your cloud resources and applications. For applications that run in the cloud, you will need access to logging and auditing services to help you proactively monitor your resources and applications


## Cloud Trail
**Cloud Trail** allows you to audit (or review) everything that occurs in your AWS account. Cloud Trail does this by recording all the AWS API calls occurring in your account and delivering a log file to you

_Features_:
- who has logged in
- services that were accessed
- actions performed
- parameters for the actions
- responses returned


## Cloud Watch
**Cloud Watch** is a service that monitors resources and applications that run on AWS by collecting data in the form of logs, metrics, and events

_Features_:
- collect and track metrics
- collect and monitor log files
- set alarms and create triggers to run your AWS resources
- react to changes in your AWS resources


## Infrastructure as Code
**Infrastructure as Code** allows you to describe and provision all the infrastructure resources in your cloud environment. You can stand up servers, databases, runtime parameters, resources, etc. based on scripts that you write. Infrastructure as Code is a time-saving feature because it allows you to provision (or stand up) resources in a reproducible way


## Cloud Formation
**AWS Cloud Formation** allows you to model your entire infrastructure in a text file template allowing you to provision AWS resources based on the scripts you write


## Global Infrastructure
**Region** - a region is considered a geographic location or an area on a map
**Availability Zone** - an availability zone is an isolated location within a geographic region and is a physical data center within a specific region
**Edge Location** - an edge location is as a mini-data center used solely to cache large data files closer to a user's location

_Notes_:
- there are more Availability Zones (AZs) than there are Regions
- there should be at least two AZs per Region
- each region is located in a separate geographic area
- AZs are distinct locations that are engineered to be isolated from failures


## Shared Responsibility Model

AWS is responsible for security **OF the cloud**, we are responsible for security **IN the cloud**

_AWS is responsible for_:
- securing edge locations
- monitoring physical device security
- providing physical access control to hardware/software
- database patching
- discarding physical storage devices

_You are responsible for_:
- managing AWS Identity and Access Management (IAM) 
- encrypting data
- preventing or detecting when an AWS account has been compromised
- restricting access to AWS services to only those users who need it

# Foundational and Compute Service

## Elastic Cloud Compute
**Elastic Cloud Compute** or **EC2** is a foundational piece of AWS' cloud computing platform and is a service that provides servers for rent in the cloud

_Pricing Options_:
1. On Demand - pay as you go, no contract
2. Dedicated Hosts - you have your own dedicated hardware and don't share it with others
3. spot - you place a bid on an instance price, if there is extra capacity that falls below your bid, an EC2 instance is provisioned, if the price goes above your bid while the instance is running, the instance is terminated
3. Reserved Instances - you earn huge discounts if you pay up front and sign a 1-year or 3-year contract


## Elastic Block Store
**Elastic Block Store (EBS)** is a storage solution for EC2 instances and is a physical hard drive that is attached to the EC2 instance to increase storage

## Virtual Private Cloud (VPC)
**Virtual Private Cloud (VPC)** allows you to create your own private network in the cloud. You can launch services, like EC2, inside of that private network. A VPC spans all the Availability Zones in the region

VPC allows you to control your virtual networking environment, which includes:
- IP address ranges
- subnets
- route tables
- network gateways


## Lambda
**AWS Lambda** provides you with computing power in the cloud by allowing you to execute code without standing up or managing servers. 

- the code you run on AWS Lambda is called a “Lambda function” 
- Lambda code can be triggered by other AWS services
- AWS Lambda supports Java, Go, PowerShell, Node.js, C#/.NET, Python, and Ruby 
- there is a Runtime API that allows you to use other programming languages to author your functions 
- Lambda code can be authored via the console


## Elastic Beanstalk
**Elastic Beanstalk** is an orchestration service that allows you to deploy a web application at the touch of a button by spinning up (or provisioning) all of the services that you need to run your application. Elastic Beanstalk can be used to deployed web applications developed with Java, .NET, PHP, Node.js, Python, Ruby, Go, and Docker. You can run your applications in a VPC.

# Storage and content delivery

## S3 & S3 Glacier
**Amazon Simple Storage Service (S3)** is an object storage system in the cloud. S3 offers several storage classes, which are different data access levels for your data at certain price points

_Storage Classes_:
- S3 Standard
- S3 Glacier
- S3 Glacier Deep Archive
- S3 Intelligent-Tiering
- S3 Standard Infrequent Access
- S3 One Zone-Infrequent Access


## DynamoDB
**DynamoDB** is a NoSQL document database service that is fully managed. Unlike traditional databases, NoSQL databases, are schema-less. Schema-less simply means that the database doesn't contain a fixed (or rigid) data structure

- DynamoDB can handle more than 10 trillion requests per day
- DynamoDB is serverless as there are no servers to provision, patch, or manage
- DynamoDB supports key-value and document data models
- DynamoDB synchronously replicates data across three AZs in an AWS Region
- DynamoDB supports GET/PUT operations using a primary key


## Relational Database Service (RDS)
**RDS (Relational Database Service)** is a service that aids in the administration and management of databases. RDS assists with database administrative tasks that include upgrades, patching, installs, backups, monitoring, performance checks, security, etc.


## Redshift
**Redshift** is a cloud data warehousing service to help companies manage big data. Redshift allows you to run fast queries against your data using SQL, ETL, and BI tools. Redshift stores data in a column format to aid in fast querying

- Redshift delivers great performance by using machine learning
- Redshift Spectrum is a feature that enables you to run queries against data in Amazon S3
- Redshift encrypts and keeps your data secure in transit and at rest
- Redshift clusters can be isolated using Amazon Virtual Private Cloud (VPC)

# Content Delivery In The Cloud
A **Content Delivery Network (CDN)** speeds up delivery of your static and dynamic web content by caching content in an Edge Location close to your user base.


## Cloud Front
**CloudFront** is used as a global content delivery network (CDN). Cloud Front speeds up the delivery of your content through Amazon's worldwide network of mini-data centers called Edge Locations

- amazon countinously adds new Edge Locations
- cloudFront ensures that end-user requests are served from the closest edge location
- cloudFront works with non-AWS origin sources
- you can use GeoIP blocking to serve content (or not serve content) to specific countries
- cache control headers determine how frequently CloudFront needs to check the origin for an updated version your file
- the maximum size of a single file that can be delivered through Amazon CloudFront is 20 GB

# Security In The Cloud
As adoption of cloud services has increased, so has the need for increased security in the cloud. The great thing about cloud security is that it not only protects data, it also protects applications that access the data. Cloud security even protects the infrastructure (like servers) that applications run on

## AWS Shield
**AWS Shield** is a managed DDoS (or Distributed Denial of Service) protection service that safeguards web applications running on AWS. AWS Shield is a service that you get "out of the box", it is always running (automatically) and is a part of the free standard tier. If you want to use some of the more advanced features, you'll have to utilize the paid tier


## AWS WAF
**AWS WAF (AWS Web Application Firewall)** provides a firewall that protects your web applications. WAF can stop common web attacks by reviewing the data being sent to your application and stopping well-known attacks

- WAF can protect web sites not hosted in AWS through Cloud Front.
- you can configure CloudFront to present a custom error page when requests are blocked


## Identity & Access Management
**Identity & Access Management (IAM)** is an AWS service that allows us to configure who can access our AWS account, services, or even applications running in our account. IAM is a global service and is automatically available across ALL regions


# Networking
Networks reliably carry loads of data around the globe allowing for the delivery of content and applications with high availability. The network is the foundation of your infrastructure

Cloud networking includes:

- network architecture
- network connectivity
- application delivery
- global performance
- delivery

## Route 53
**Route 53** is a cloud domain name system (DNS) service that has servers distributed around the globe used to translates human-readable names like www.google.com into the numeric IP addresses like 74.125.21.147

_Features_:
- scales automatically to manage spikes in DNS queries
- allows you to register a domain name (or manage an existing)
- routes internet traffic to the resources for your domain
- checks the health of your resources
- allows you to route users based on the user’s geographic location.


# Elasticity in the Cloud
One of the main benefits of the cloud is that it allows you to stop guessing about capacity when you need to run your applications. Sometimes you buy too much or you don't buy enough to support the running of your applications. With elasticity, your servers, databases, and application resources can automatically scale up or scale down based on load

## EC2 Auto Scaling
**EC2 Auto Scaling** is a service that monitors your EC2 instances and automatically adjusts by adding or removing EC2 instances based on conditions you define in order to maintain application availability and provide peak performance to your users

_Features_:
- automatically scale in and out based on needs
- included automatically with Amazon EC2
- automate how your Amazon EC2 instances are managed
- EC2 Auto Scaling adds instances only when needed, optimizing cost savings
- EC2 predictive scaling removes the need for manual adjustment of auto scaling parameters over time


## Elastic Load Balancing
**Elastic Load Balancing** automatically distributes incoming application traffic across multiple servers

Elastic Load Balancer is a service that:
- balances load between two or more servers
- stands in front of a web server
- provides redundancy and performance
- elastic Load Balancing works with EC2 Instances, containers, IP addresses, and Lambda functions
- you can configure Amazon EC2 instances to only accept traffic from a load balancer

# Messaging in the Cloud
There are often times that users of your applications need to be notified when certain events happen. Notifications, such as text messages or emails can be sent through services in the cloud. The use of the cloud offers benefits like lowered costs, increased storage, and flexibility


## Simple Notification Service
**Amazon Simple Notification Service (SNS)** is a cloud service that allows you to send notifications to the users of your applications. SNS allows you to decouple the notification logic from being embedded in your applications and allows notifications to be published to a large number of subscribers

_Features_:
- SNS uses a publish/subscribe model
- SNS can publish messages to Amazon SQS queues, AWS Lambda functions, and HTTP/S webhooks
- SNS Topic names are limited to 256 characters
- a notification can contain only one message


## Queues
A *queue* is a data structure that holds requests called messages. Messages in a queue are commonly processed in order, first in, first out (or FIFO). Messaging queues improve performance, scalability and user experience

## Simple Queue Service
**Amazon Simple Queue Service (SQS)** is a fully managed message queuing service that allows you to integrate queuing functionality in your application. SQS offers two types of message queues: standard and FIFO

_Features_:
- FIFO queues support up to 300 messages per second
- FIFO queues guarantee the ordering of messages 
- standard queues offer best-effort ordering but no guarantees
- standard queues deliver a message at least once, but occasionally more than one copy of a message is delivered

# Containers in the Cloud
Enterprises are adopting container technology at an explosive rate. A container consists of everything an application needs to run: the application itself and its dependencies (e.g. libraries, utilities, configuration files), all bundled into one package. Each container is an independent component that can run on its own and be moved from environment to environment


## Elastic Container Service (ECS)
**ECS** is an orchestration service used for automating deployment, scaling, and managing of your containerized applications. ECS works well with Docker containers by:
- launching and stopping Docker containers
- scaling your applications
- querying the state of your applications

_Features_:
- you can schedule long-running applications, services, and batch processeses using ECS
- docker is the only container platform supported by Amazon ECS

# AWS Management

## Infrastructure as Code
**Infrastructure as Code** allows you to describe and provision all the infrastructure resources in your cloud environment. You can stand up servers, databases, runtime parameters, resources, etc. based on scripts that you write. Infrastructure as Code is a time-saving feature because it allows you to provision (or stand up) resources in a reproducible way

## Cloud Formation
**AWS Cloud Formation** allows you to model your entire infrastructure in a text file template allowing you to provision AWS resources based on the scripts you write

## AWS Command Line Interface (CLI)
The **AWS CLI (Command Line Interface)** allows you to access and control services running in your AWS account from the command line. To use the CLI, simply download, install, and configure it