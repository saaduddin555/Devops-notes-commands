what is AWS?
Amazon web service is an online platform that provides scalable and cost-effective cloud computing solutions. AWS is a broadly adopted cloud platform that offers several on-demand operations like compute power, database storage, content delivery, etc., to help corporates scale and grow.

WHAT IS IAAS PASS SASS

SaaS
SaaS platforms involve software that is available via third-party over the Internet. 

Examples of popular SaaS providers include: 

BigCommerce.
Google Workspace, Salesforce.
Dropbox.
MailChimp.
ZenDesk.
DocuSign.
Slack.
Hubspot.
PaaS
PaaS focuses primarily on hardware and software tools available over the internet. 

Examples of popular PaaS providers include: 

AWS Elastic Beanstalk.
Heroku.
Windows Azure (mainly used as PaaS).
Force.com.
Google App Engine.
OpenShift.
Apache Stratos.
Adobe Magento Commerce Cloud.
IaaS
IaaS works primarily with cloud-based and pay-as-you-go services such as storage, networking and virtualization.

Examples of popular IaaS providers include: 

AWS EC2.
Rackspace.
Google Compute Engine (GCE).
Digital Ocean.
Microsoft Azure.
Magento 1 Enterprise Edition*.


# Bootstarpping of Ec2 instance using the scripts.
Bootstrapping AWS EC2 instance to update packages, install and start Apache HTTP Server
Bootstrapping in AWS simply means to add commands or scripts to AWS EC2’s instance User Data section that can be executed when the instance starts. It is a good automation practice to adopt to ease configuration tasks.

# what is user data in aws?
AWS userdata is the set of commands/data you can provide to a instance at launch time. For example if you are launching an ec2 instance and want to have docker installed on the newly launched ec2, than you can provide set of bash commands in the userdata field of aws ec2 config page.

# What is AMI in AWS
An Amazon Machine Image (AMI) is a master image for the creation of virtual servers -- known as EC2 instances -- in the Amazon Web Services (AWS) environment. The machine images are like templates that are configured with an operating system and other software that determine the user's operating environment.

EBS - backed Instances.
Instance Store - backed Instances.

* "EBS-Backed" Instances
An "EBS-backed" instance is an EC2 instance which uses an EBS volume as it’s root device. EBS volumes are redundant, "virtual" drives, which are not tied to any particular hardware, however they are restricted to a particular EC2 availability zone. This means that an EBS volume can move from one piece of hardware to another within the same availability zone. You can think of EBS volumes as a kind of Network Attached Storage.

If the virtual machine’s hardware fails, the EBS volume can simply be moved to another virtual machine and re-launched. In theory, you won’t lose any data.

Another benefit, is that EBS volumes can easily be backed up and duplicated. So you can take easy backup snapshots of your volumes, create new volumes and launch new EC2 instances based on those duplicate volumes.

Probably the biggest advantage "EBS-backed" instances have over "instance store" instances is that they can be stopped. When you do this, the virtual machine is shutdown and the EBS volume is stored for later retrieval. The hardware is then available for someone else to use. In addition, during this time, you are not charged the EC2 instance running charge. But you are charged for the EBS storage. When you want the instance to run again, you just start it up again. A new virtual machine is reserved, your EBS volume is attached, and your instance is booted.

But what about the virtual machine’s hard drives?

Yes, it is possible to use those hard drives, even when your EC2 instance is "EBS-backed". By default, they are not available. If you use the command line programs to launch your instance, you can use the "-b" option on the ec2-run-instances command to attach the "instance store" drives to your EC2 instance.

Having these drives available can be beneficial if you want to store temporary data. Read and write access should be faster than reading from and writing to an EBS volume because you’re not sending data over the network. In addition, you won’t be charged for data transfer or data storage. But this only works if the data can be lost at any time.

* "Instance Store" Instances
An "instance store" instance is an EC2 instance whose root device resides on the virtual machine’s hard drive. When the instance is created, the base AMI is copied to the virtual machine’s hard drive and launched. The instance can run for as long as you want, but it cannot be stopped. Since the instance’s root device is the actual hard drive, it is "stuck" on the hardware, and the only thing you can do is terminate the instance. If you do this, the instance is deleted, never to be recovered. You also run the risk that if the virtual machine’s hardware fails, then you will also lose anything on the hard drive.

If you launch an "instance store" instance, be prepared to leave it running until you’re completely done with it. Note that you will be charged from the moment the instance is started, until the time it is terminated.

# What is secretkey and access key

An access key grants programmatic access to your resources. This means that you must guard the access key as carefully as the AWS account root user sign-in credentials. It's a best practice to do the following: Create an IAM user, and then define that user's permissions as narrowly as possible.

AWS Access Keys
Access Keys are used to sign the requests you send to Amazon S3. Like the Username/Password pair you use to access your AWS Management Console, Access Key Id and Secret Access Key are used for programmatic (API) access to AWS services.

Root Access Keys
Root Access Keys provide unlimited access to your AWS resources. It's not recommended to use them in normal situations. AWS recommends to delete existing Root Access Keys and create IAM user and Access Keys limited to specific service or resource (see below).

To Delete Root Access Keys
1. Type aws.amazon.com in your web browser

2. Click My Account, Security Credentials

3. Enter your account email address and password:

You will be redirected to the Your Security Credentials page of the IAM service.

4. Expand the Access Keys (access key id and secret access key) section.

5. Click the Delete link next to your access keys.

Secret access keys are—as the name implies—secrets, like your password. For your own security, AWS doesn't reveal your password to you if you forgot it (you'd have to set a new password). Similarly, AWS does not allow retrieval of a secret access key after its initial creation.

# What is the use of security group
A security group acts as a virtual firewall, controlling the traffic that is allowed to reach and leave the resources that it is associated with. For example, after you associate a security group with an EC2 instance, it controls the inbound and outbound traffic for the instance.

AWS Security Groups help you secure your cloud environment by controlling how traffic will be allowed into your EC2 machines. With Security Groups, you can ensure that all the traffic that flows at the instance level is only through your established ports and protocols.

Distribution groups are used for sending email notifications to a group of people. Security groups are used for granting access to resources such as SharePoint sites. Mail-enabled security groups are used for granting access to resources such as SharePoint, and emailing notifications to those users

Security groups provide a kind of network-based blocking mechanism that firewalls also provide. Security groups, however, are easier to manage. Firewalls are generally configured with IP-specific rules, such as allowing or blocking traffic on a specific port or accepting traffic from a particular server.

# what are the different services using in AWS


# What is exactly Ec2 Does??
Amazon Elastic Compute Cloud (Amazon EC2) provides scalable computing capacity in the Amazon Web Services (AWS) Cloud. Using Amazon EC2 eliminates your need to invest in hardware up front, so you can develop and deploy applications faster.

# Have you work on AWS CLI
No

# What are the difference between scalability and elasticity

# What is EBS

# can we mount 1EBs to Multiple EC2 Instances, If not what is the solution for this?

# can we attach EBS TO EC2 Which are different Az but which are in same region?

# what is EFS

# Purpose and use of S3

# What is the file size limit in s3?

# what is ROute53?


# What is difference between private and Public subnet.

# How to access internet on private subnet?

# What is NAT Instance and  NAT Gateway.

# Components of VPC

# Types of storage in AWS

# Difference between s3 and Glacier

# Different types of storage in s3?

# What is Glacier and snowball?

# what is autoscaling

# what is Region and availability zone?

# What is cloud watch

# Differnce between NACL and security group.

# S3 Lifecycle

# what is ststic or elastic Ip

# How do you connect to windows instances in AWS

# what is difference between EBS,s3 and EFS?

# If you lost the pen key how will you connect to EC2 Instance?

# What is IAM?

# How will you attach policy for IAM users by group or Individual?

# Types of Load Balancer and Example?

# can we route request to EC2 which are running in different regions where as ELB is in different regions using only ELB? If not what is the solution for this...


DevOps Interview Questions AWS
Define and describe the usage of:
DevOps in Amazon Web Services (AWS)
AWS Lambda
Code Commit
Continuous Integration (CI)
Continuous Delivery (CD)
AWS Code Build 
CodeDeploy
CodePipeline
Amazon Machine Image
Hybrid cloud
Virtual Private Cloud (VPC)
VPC Peering
VPC Endpoints
EBS (Elastic Block Storage)
Infrastructure as Code (IaC) 
Microservices
AWS CloudFormation
Auto-scaling
Amazon Elastic Compute Cloud
Differentiate between:
AWS CloudFormation and AWS Elastic Beanstalk
Scalability And Elasticity
DevOps and Agile
classic automation and orchestration

AWS DevOps Engineer Interview Questions
Name and describe the core components of DevOps.
What does DevOps help in accomplishing?
Name a real-life example where DevOps can be implemented.
How can we implement IaC by using AWS?
State some challenges associated with creating DevOps pipelines and describe how you’d deal with them.
Name the security laws that we implement to secure data in a cloud.
Describe the two data centers that are deployed for cloud computing.
Describe the different components used in AWS.
How would you handle revision control?
How can we build a hybrid cloud?
In the context of infrastructure, describe configuration management.
What are the different layers that define Cloud Architecture?
Name the different deployment models for the cloud.
What is the relationship between instance and AMI?
What automation tools can we use to spin up servers?


Q1. Name some common top DevOps tools.
Some top DevOps tools are Chef, Puppet, and Ansible as Configuration Management and Deployment Tools, Git as a Version Control System Tool, Jenkins as a Continuous Integration Tool, Docker as an effective Containerization Tool, and Nagios as a Continuous Monitoring Tool.

Q2. What is the role of a DevOps engineer? 
DevOps engineers use DevOps practices to simplify the software development process. They build, test, and maintain the infrastructure and tools and enable efficient software development and release. Working alongside developers and IT staff, a DevOps engineer oversees code releases in their company.

Q3. What is the difference between DevOps and Agile?
Despite the significant overlap between DevOps and Agile, the main difference is that Agile focuses on seamless software development or production. In contrast, DevOps focuses on efficient and reliable software development and deployment.

Q4. Name the two data centers deployed for cloud computing.
Containerized and low-density data centers are the two types deployed for cloud computing.

Q5. Can you share a single instance of Memcache among multiple projects?
Yes, since Memcache is a storage space that different projects can share, we can share a single instance of Memcache between multiple projects

ActiveMQ vs Memcached: What are the differences?

Developers describe ActiveMQ as "A message broker written in Java together with a full JMS client". Apache ActiveMQ is fast, supports many Cross Language Clients and Protocols, comes with easy to use Enterprise Integration Patterns and many advanced features while fully supporting JMS 1.1 and J2EE 1.4. Apache ActiveMQ is released under the Apache 2.0 License. On the other hand, Memcached is detailed as "High-performance, distributed memory object caching system". Memcached is an in-memory key-value store for small chunks of arbitrary data (strings, objects) from results of database calls, API calls, or page rendering.

ActiveMQ belongs to "Message Queue" category of the tech stack, while Memcached can be primarily classified under "Databases".

What is Memcached?
Memcached is an in-memory key-value store for small chunks of arbitrary data (strings, objects) from results of database calls, API calls, or page rendering.









