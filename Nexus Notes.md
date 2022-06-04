# Nexus

Nexus is an Artifactory Repository tool

Popular Artifactory Repository tools:

* Sonatype Nexus

* Jfrog Artifactory

These are used to store the build Artifacts or packages..

Nexus is an open source Java based artifactory repository manager
It can be used to store the build artifacts and retrive the build artifacts when ever we required.

What is the difference between Github and Nexus

Github is an source is an source code management tool and Nexus is Artifactory Repository manager, it is used to store the build Artifacts.

can we store jar/war/ear in github ...Yes but it is not the good practice...

Nexus has two Edition

OSS --- Opensource software
Nexus prod  -------- Enterprise Edition

If it is a Java we create Jar,war,ear 

DOcker--- Docker Images

NodeJs ----.tar file

Using Nexus we can store any other programming languages packages also

# Nexus Architecture

bin: Binary files

lib: library files

etc: Instead of conf directory we have etc directory.
      nexus-default.properties is imp file to do configuration in nexus

# Nexus installation

pre-requisistes---Java

Nexus 3.x ---- JAVA 1.8 or java 8 is need for nexus 3.xxx and above

Minimum 1gb ram is required and 1 gb ram for Os totally 2gb ram is required to run Nexus server


##Login as a root user
sudo su -

##Change dir to /opt 
cd /opt
yum install wget -y
wget -c --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u131-b11/d54c1d3a095b4ff2b6607d096fa80163/jdk-8u131-linux-x64.rpm
yum install jdk-8u131-linux-x64.rpm -y

java -version

Login as a root user
sudo su -
cd /opt
yum install tar wget -y
wget http://download.sonatype.com/nexus/3/nexus-3.15.2-01-unix.tar.gz
tar -zxvf nexus-3.15.2-01-unix.tar.gz
mv /opt/nexus-3.15.2-01 /opt/nexus

#As a good security practice, Nexus is not advised to run nexus service as a root user, so create a new user called nexus and grant sudo access to manage nexus services as follows.
 
useradd nexus

#Give the sudo access to nexus user

visudo
nexus ALL=(ALL) NOPASSWD: ALL

#Change the owner and group permissions to /opt/nexus and /opt/sonatype-work directories.

chown -R nexus:nexus /opt/nexus
chown -R nexus:nexus /opt/sonatype-work
chmod -R 775 /opt/nexus
chmod -R 775 /opt/sonatype-work

#Open /opt/nexus/bin/nexus.rc file and  uncomment run_as_user parameter and set as nexus user.

vi /opt/nexus/bin/nexus.rc
run_as_user="nexus"

#Create nexus as a service

ln -s /opt/nexus/bin/nexus /etc/init.d/nexus

#Switch as a nexus user and start the nexus service as follows.

su - nexus

#Enable the nexus services
sudo systemctl enable nexus

#Start the nexus service
sudo systemctl start nexus

#Access the Nexus server from Laptop/Desktop browser.
 
http://IPAddess/Hostname:8081/

#Default Credentials
User Name: admin
Password: admin123
Your admin password is located at in  /opt/sonatype-work/nexus3/admin.password on the server

Troubleshooting
---------------------
nexus service is not starting?

a)make sure need to change the ownership and group to /opt/nexus and /opt/sonatype-work directories and permissions (775) for nexus user.
b)make sure you are trying to start nexus service with nexus user.
c)check java is installed or not using java -version command.
d) check the nexus.log file which is availabe in  /opt/sonatype-work/nexus3/log  directory.

Unable to access nexus URL?
-------------------------------------
a)make sure port 8081 is opened in security groups in AWS ec2 instance.

* Always refer Nexus Doumentation site and Downloads to download updated Package and Instruction also...


# PUSH/PULL Docker Image form Private Repository (Nexus)
Pre-Requisities:
Server 1: Ubuntu                                         Server 2: Ubuntu
Install the below softwares in Server1          Install the below softwares in Server2
Java 8                                                              Docker

Docker

Jenkins

Maven/Gradle
Server 1:
1   We are going to build our project using maven/gradle
2   Through docker file we are going to create an docker image for that project
3   We are going to push the docker image to Nexus (docker hosted) repo
Server 2:
1  We are going to pull the docker image form Nexus (docker hosted) repo
2   Create a container using the docker image
Nexus Repository (docker hosted,proxy) Creation:
docker hosted:   
1) Login to your Nexus repository.
2) Create docker hosted

Here give a name to the repo (dock-hosted), then we are going to assign a port to this docker hosted repo. Through this port we are going to access this repo. (Note: you should not give 8081 because it is already assigned to Nexus Repo, so use different port number)

In this case I have assigned 8083 for this repo.

3) Keep the remaining settings as it is and create repository

Note: Open 8083 in AWS Security Groups.
Ubuntu Configuration : Server 1 & 2
Do these steps in both the servers in order to push and pull docker images from Nexus Repo.
1.     Login as root user
2.     Go to /etc/docker
            cd /etc/docker
3.     Then create a file called daemon.json
vi /etc/docker/daemon.json
4.     Write these script in daemon.json

{
  "insecure-registries": [ "13.234.21.143:8083" ]
}

(Here we are allowing our docker daemon to access the Nexus Hosted Repo)
5.     Save the file
6.     Restart docker service using below command.
            systemctl restart docker

 
Server 1: Login,Build & Push
1 Login to Nexus repo
docker login –u admin –p password 13.234.21.143:8083
(or)
docker login 13.234.21.143:8083

2  Build an image using below command.
docker build –t 13.234.21.143:8083/image1 .
           
(here while building an docker image we will use ip address with port for the docked hosted repo instead of username in hub.docker.com)

3 Push docker image to Nexus Repo

Server 2: Pull image/Run container
1.     Login to Nexus

2   Pull docker image


3  Build a container
docker run –d –p 8090:8080 –p 9990:9990 - -name wildfly 13.234.21.143:8083/image1
(I am using wildfly to deploy)     

# nexus-default.properties

cd /opt/nexus/etc/

In this file nexus-default.properties we can configure and do changes related to port numbers, context path etc for nexus server

The default port no is 8081

service nexus restart

# default repositories in Nexus are

Maven central
maven public
maven releases
maven snapshots
nuget group
nuget hosted
nuget.org-proxy

# How to Create a repo in Nexus

In Nexus click on create Repo and fill the details like 

Name
Online check/

version policy: Releae/snapshot/mixed

create


...

Click on browser content tab to browse repository..

A New project is on boarded on It, we need to create two repositories

release and snapshot

# Where we are going to configure Nexus Repo details

In which Tag

<distributionManagment>

  <repository>
  <id>nexus<id>
  <name>Facebook Releases Nexus repo</name>
  <url>Facebook releases repo url</ur/>
  </repository>

  <snapshotRepository>
   <id>nexus</id>
   <name>Facebook_snapshot_Nexus_Repository</name>
   <url>facebookrepo_snapshot_url</url>
   </snapshorRepository>

</distributionManagment>

# Where we are going to configure credentials for nexus

In settings.xml using Userid and password and repo link

<servers>

   <server>

   <id>nexus</id>

   <username>admin</username>
   <password>admin123</password>

   </server>

</servers>

In real time we use Elastic_IP and attach to server even nexus restarts, it is not going to change the public_Ip 
as we configured above Urls, when AWS server restarts, it makes an issue to server..

# How to Upload packages into remote repository

mvn deploy        Is the goal to deploy into nexus repository or any remote repo.
vs
mvn install       Is the goal to store war/jar into maven local repo.

What are the goals which execute for mvn deploy

validate
compile
test
package
install
deploy

we can use Generated package which is stored in Nexus as dependency to another project using snippet which is generated in 
Nexus server UI

Go to browse.....>click on project snapshot.........>click on war file and scroll down to see all info and snippet details also..

<dependecy>
</dependency>

The snippet looks like this to paste in pom.xml file..

Each build is uploaded to directory with n number of times it deploy as if it is configured as snapshot version...

It Uploads in Snapshot repo everytime a package is built n number of times, the package builds..

Snapshot repository contains on going development packages....

403 error means ....forbidden not enough access user access

401 means .....Unauthorized check credentials 

# when it uploads to repo??? as we configured repo also ...

SNAPSHOT

RELEASE 

if we give in uppercase as above in version it uploads to such repositories...

The production releases, the production packages are going to store in releases repository..

All production version will contains releases repositories..

<version>0.0.1-snapshot</version>

If a version tag contains snapshot keyword it uploads to snapshot repository

<version>1.0.0</version>

if version tag contains only version number keyword it uploads to releases repository.

If we upload/deploy again with same 1.0.0 version will it Upload????

We will get the error...

we got 400 error 

what is 400 error??? its Bad Request, you are not sending proper request.

All 400 series issues are client side issue

The releases version are not going to Override in releases repo

To fix this you need to change the version in pom.xml as 2.0.0 version as we are deploying the package same again...

# How to Override to releases forcefully

Go Nexus admin repo page

click on releases repo

click on deployment policies

By default deployment policy is disabled

Allow redeploy and save it.....

mvn clean deploy...

It will allow u to upload same version..

and u can change it to default after re-deploying..

Created and Updated Timestamp changes if any force updates is done.

# There are two Tabs

Browse Tab..........Settings Tab.........search.............refresh....admin....signout

If you want to browse in repo click on browse tab

If you want to do settings for the repo click on settings tab

# Maven Repositories.

Maven Local repo

Maven Central Repo

Remote repo


# I want to share 10 jar files to my team how can i acheive it and how to create REMOTE repository???

Create New Repo

settings 

version control as Mixed

and create the Repo

If a package file is in server how can i download it to my laptop as i want to update to that Nexus repo

use Any FTP tool

Use Filezilla or any FTP tool

First Copy maven jar file to Temp or home directory..

After downloading

Go to Nexus...select repo

Click on upload file and manually, u can upload any file in Nexus..

enter details for artifact:

File.....

componentes coordinates

GroupID: com.facebook-build name,artifact,version...

Artifact id: 

Version:


# What is the command to upload external package build artifact to the Repository

mvn deploy:deploy-file

Now we dont need to execute as we have GUI upload feature as mentioned steps above..

# WHat is Maven2 Proxy Repository??

In Maven central repository when ever a download of dependencies happens, It may also contain harmful Viruses also

I dont want to donwload dependencies directly from maven central repo

From central repo it download goes to proxy remote repository such as which we configure in Nexus or Jfrog 

The repository servers are usally Linux based server, They are good to remove viruses using Antiviruses tool which are pre built..

From Remote repo we will be using to Local Repo..

If something is not available in Proxy remote repo...??

The request goes to Central and redirects to remote repo and to Local

Steps:

Go to Nexus

Create Repsoitory

Click on Maven2Proxy

Name:

Verison: Mixed

Remote-repo-Storage: Here we need to give Maven central repository Url.

scroll down and leave all default settings

-----

--

HTTp:

Authentication: Check box if your repo is secured one...


create repo..

Configure Proxy repo in POM.XML and Settings.XML


<repository>
<id>nexus</id>
<name>Remote Repo Proxy</name>
<url>http://............../repo/proxy-remote/repo/</url>
</repository>

Configure in settings.xml

<mirrors>

<mirror>
<id>nexus</id>
<mirrorof>leaveitdefaut</mirrorof>
<name></name>
<url>Give That Proxy repo Url</url>
</mirror>

</mirrors>


<localRepository>/root/mvnlocalrepo/</localRepository>


This will check in local and proxy and if local repo doesnt contain any dependencies, it will search in proxy and central to proxy to local.


Note: In Pom.xml and settinsg.xml we configure local and proxy details as above

but how does central repo is in contact ?? As we will configure in Nexus Remote proxy repo..

# Create a Group Repo 

As we can acess all the repo which are in group and part of it..

maven2group

Mixed

Add all the repo which are pre existed to group

such as proxy, central, remote and etc and create a group.

No we got Group Repo Url

Add the Url in Pom.xml and settings.xml what ever the resources are not available it will find in group repo which all repo are listed.

Configure group repo in POM.XML and Settings.XML


<repository>
<id>nexus</id>
<name>Remote Repo group</name>
<url>http://............../repo/group-remote/repo/</url>
</repository>

Configure in settings.xml

<mirrors>

<mirror>
<id>nexus</id>
<mirrorof>leaveitdefaut</mirrorof>
<name></name>
<url>Give That group repo Url</url>
</mirror>

</mirrors>

save it\\

go to project folder and execute we will get all repo packages now...Multipule repo config.

Later also we can add or remove repositories later also..

we use generally Group repo in pom.xml configurations..

# Administration..

* Repositories: We can create/delete/update about repositories.

* Blob Storage: Blob is a datatype to store the images or files, such as large objects.
Varchar
varchar2
we are storing here the Artifacts.
we can create a Blob Store, In local(Nexus file system) or S3(Simple storage service) Bucket also...
The Blob storage path in local nexus sever:
/opt/sonatype-work/nexus3/blobs/name_of_blob
we can use blobstrage to store docker images and various images...


* Cleanup policies: Cleanup Policies can used to remove content from repositories
These can be configured, iNstead of manually going and deleting, we can atatch the cleanup policies to repository.
If the policies matched then the policies are going to delete...
like
component Age.....Days
Component Usage....Remove components that have not been downloaded 

Preview Repository: to preview what is going to be deleted

save it...

go to repo and add cleanup policy

and save it

The Cleanup Policy is scheduled for the time and deletes from nexus..



* Security: Create Users with Id and Passwords, email, Active
Roles:
   nx-admin: He has all access.
   nx-anaonymous: Only he can see repo and browse only..
   and save..
we can manualy create Roles: and give manually access to roles what users is allotted..

Anonymous Acess: Enable means anyone can access to repo without userid and password..

LDAP: We can use LDAP in real time called as LDAP(Light weight directory access protocol) to login Server..
      Employee Info
      Employee Name
      Employee Password.

      what ever details is created with LDAP server we can integrate and configure..

SSL Certificates: If we want to use servers secure we use SSL certificates, we need to purchase the SSL Certificates.
We can Purchase these certificates from certificate provider the popular company is CA

* Support: All logs and Logging is generated and can be downlaoded for troubleshootings of server
  Status: The System health and Usage of the server indications will be shown
  green--Normal   Red---Critical issues.
  All the errors related to ssytem with notifications will be shown.
  Support_ZIP:It wil create a zip file of log files related to the server
  System Information: All System Info is displayed here

System:
Licensing: To Buy Licensing feature is going to enable pro features..
           Oss features will be Pro Edition
           Just paste and install License
API: 
    Using API we can connect to server Programmitically using API
    we can do operations using CLI and write some scripts to automate tasks using CLI
    There are references in Nexus and can use and try it out features to specific usecase..
    It generates CLI snippet and copy and paste to work..
    we can call these API in browsers also.

HTTP METHODS

GET: To GET SOME INFO from Server

POST: To Create some resources in server

Delete: Delete some Information in server

PUT: To Update Information in server



404----Error Not found
204---Repository deleted
401---Authentication required
403--Insufficient permissions.

-----------------------------------------------------------------------------------------------------------------------------------------

