# Aws Notes
AWS Security Groups
AWS MFA
AWS IAM
AWS Budgets
slack tool for budget alerts
VPC
subnets
CIDR:Classless inter-domain routing (CIDR) is a set of Internet protocol (IP) standards that is used to create unique identifiers for networks and individual devices. The IP addresses allow particular information packets to be sent to specific computers.
-cidr.xyz to know range of ip address of CIDR
Internet gateway
NAT gateway:To allow interconnectin between two subnets
NACl:(network ACL)
A firewall to controll traffic from and to subnet which can allow and deny rules, Are attached to subnets and rules includes only ip address
VPC logs: to gets logs and issues reagrding VPC
VPC peering: connect one or more VPC and give access to one and other as id they are in same network


### Virtual Machines(AWS EC2)
EBS Volumes and Optimizations
Images
Snapshots
Network load balancers
Application Load Balancer
Autoscaling Groups

Amazon Machine Image(AMI): It is a template which contains all sort of software configurations such as operating systems,application server and aplications required to launch an instance, For every Image there will be an Amazon Id and by default it will be given to it. The AMI can be selected from the following below

                    Quick start: Default AMI such as Amazon, ubuntu,redhat etc free tire Images.

                    My AMIs: The AMI which is saved by an user after doing certain tweaks such as updates,patches,installations and saving additional configuration as an images are My AMI Images.

                    Aws Market place: The Market place contains Any other type of images which can be free or purchased 

                    Community AMI: The Images which is Shared by Community called as Community AMI.

### Instances: 
Instance is a virtual server in the AWS Cloud. With Amazon EC2, you can set up and configure the operating system and applications that run on your instance. When you sign up for AWS, you can get started with Amazon EC2 using the AWS Free Tier .Instances are Virtual computing power as same as CPU where a user or organisation can utilize the computing power and resources virtually.

          General Purpose 
          Compute Optimized
          Memory Optimized
          Accelerated computing
          Storage Optimized
          Insatnce Features
          Measuring Instance Performance

The Compute families are called as t1,t2,t3,t4,t5...m1,m2,m3,m4,m5....r1,r2,r3,r4,r5....etc are families of virtual servers
The Intsance types also depends up on old technology to new technology usage of hardware
The netwok speed also varies from instance type to instance type.

### Limits:
In AWS For every service there is limits of launch and usage of services as hence always recommended to check the limits of AWS services
we can raise a ticket for few services to raise the limits for the AWS Account 
depends from service to service.

### Placement groups: 
Placement group determines how the insatnces are placed on underlying hardware.A clusture Placement group clustures instances into low-latency group in a single Availability zone. 
A partion placement group spread instances across logical partitions, ensuring that instances in one partition do not share underlying hardware with the instances in other partitions. 
A spread placement group spreads instances accross underlying hardware. can use spread if we more than 7 instances. 

### Launch Templets: 
Deploys only virtual machines in existing VPC. The repeted task will make easier using Launch templetes, The launch instances help to automate the task by using amazon cli or aws cloud cli and automate bulk instance launches.
* Create a Launch templete in AWS Console and configure it, dont confiure Subnets just configure security group in networking and do rest settings and you will get launch templete id. make sure u create subnets previously in VPC.
* The Configure of Subnets in launch templete makes to create multiple instances to launch in same subnet as hence we using automation 
method to create and launch instances templetes and subnets.
* Open Aws Cloud CLI 

Automating of launching instance using aws CLI using launch templetes id.

#!/bin/bash
I=1
for subnet in 'subnet-give subnet id here' 'subnet-give subnet id here' 'subnet-give subnet id here'
do
echo "Creating EC2 Instance using subnets"
aws ec2 run-instances --launch-template LaunchTemplateId=give_launch_template_id_here --subnet-id $subnet --tag-specifications 'ResourceType=insatnce,Tags=[{Key=Name,Value=Testserver-'${I}'}]'
I=$((I+1))
done

### Types of Instances Opt to use: Spot request

On demand Instance: regular way of launching the server

Spot Instances: To check in discounted rates of launching the server, basically temporary untill demand comes gives 10 min time to backup and terminates.we can use this instance in test purposes or webservers running or autoscalling config, not for crucila database servers.

Reserve Instances: Reserving Instances for months to years and save cost in discount offer an pay Upfront or partial cost and own the server.

Scheduled Instances: To schedule an instance for period of time either by week or days

### Savings Plans:
Saving Plans are Flexible pricing model that offers low prices on EC2, Fargate and Lamda Usage in Exchange for commitment to consistent amount of usage measured in hours for a 1 to 3 year term. Saving Plans provide you flexibility to use compute option that best suits and automatically save money.

### Elastic block storage
Volumes
snapshots
Lifecycle Manager

Volumes: we can create volumes and attach those volumes u the existing Instances.
The disks wiil be in the form of Raw fomat hence, need to format the disk 
#lsblk in linux to access the disks
raw>>>partition>>>filesystem>>>>mount
fdisk /dev/xvdf
n for new partion, press enter 4 times
w for format the partion, The new partion is created.

mkfs.ext4 /dev/xvdf1  (To create file System in Linux)
mkdir /datavol1        (to create a folder)
lsblk                   (To access disk info)
mount /dev/xvdf1 /datavol1/   (To mount a volume)
df -h                         (To check volumes and partition information)

always add disk details in etc/fstab tab to fix the disk permanently to os or else reboot will erase the details.

nano /etc/fstab
edit the file and add new disk config

/dev/xvdf1         /datavol1/       ext4        defaults,noatime    1   1

and save the file

df -h (To check volumes and partition information)
mount -a ( to Mount a volume agian)
cd datavol1

Now You can create a new file.

# TO increase partition for existing drive where drive is unallocated or increased space in AWS.
lsblk to get list of drives and names
growpart /dev/nameofdisk                (To increase the drive capacity)

growpart /dev/xvdf 1                    (here 1 indicates partition number)

lsblk

Resize file system also

resize2fs /dev/xvdf1                            (To resize file system also)

df-h (To check the drive details)


# Different types of EBS volumes












