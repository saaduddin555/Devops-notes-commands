# Tomcat

In Maven we have Created three Packages JAR,WAR and EAR

so for running the jar file we can use JAVA command

java -jar jarfilename   (For running jar file)

If we want to run java class

java helloWorld

For WAR and WAR can we run using JAVA command???? NO

We have to use Application servers to deploy the applications in order to run WAR and EAR files...

# What are the Popular Application server are there????

Websphere Application server (WAS)
WebsSphere Liberty Profile
IBM is Provider of these two servers

Weblogic .......BEA .....>Oracle

Few companies are using these licensed applications like WAS and Weblogic by CITIBANK, HDFC and few ecommerce companies...

Opensource:

JBoss/Wildfly........>Redhat.......>IBM

Apache TOmcat.......>Apache software foundation

Use these application servers to deploy war/ear files

If want to use these applications you need purchase license and leaving Apache Tomcat and Wildfly as it is Opensource

Apache Tomcat is open source, JAVA based Application server:
Tomcat only supports JAVA based Applications

All the above servers work only JAVA language.....

FOr
NodeJS/Angular............>TO Run the Nodejs/Angular Applications install Node/Angular software in system.
Python.................>Python softwares to run the Python applications is needed
.NET....................>IIS 

# Tomcat
Tomcat is open source Java based, Web application server
The Tomcat Only support web applications

It is not going to support Enterprise Applications like EAR files...

so Assume we have developed EAR Applications, where we can host, we can host and deploy in to Any one of servers like

Websphere Application server
Websphere Liberty profile
WEblogic
JBoss/Wildfly

These servers are going to support WAR/EAR also 

But in Tomcat we can deploy only WAR

SO if you want to Explore JBOSS/WIldfly Application refer Youtube channel of Mithun Technologies for installation/deloyment and more details..

# Tomcat server Directory Structure...

To install tomcat go to https://tomcat.apache.org/download

Download from Binary distribution

Select zip or tar.......for linux

32 or 64 for windows/service insatller, it is going to download exe file..

SOurce code Distribution are used to Development and add new features for tomcat...

* In real time we use zip or tar file for linux servers

Once you extract zip or tar files you will going to see the directories and it will be going to work any of os and see the details

we see After Extraction

bin: It contains Binary files like startup.sh, startup.bat, shutdown.sh, shutdown.bat 
     startup.sh: used to start the tomcat server in mac book or linux, startup.bat is used t run in WIndows
     shutdown.sh used to stop the linux and mac, shutdown.bat is for windows

     catalina.sh: It is used to start or stop the linux and mac server
     catalina.bat: It is used to start or stop the Windows server

* How to use the files
    sh catalina.sh start
    sh catalina.sh stop 
    sh startup.sh
    sh shutdown.sh

    we have version.sh and version.bat to check versions

conf: This Directory we have configuration files, such as which are important
      
      servers.xml
      tomcat-users.xml

lib: The lib directory contains JAR files which are called as libraries...Any JAVA software which contains lib files are libraries,JAR files 
     helps to run the softwarre

logs: In logs we have various files such as:
       Manager.log
       hostmanager.log
       catalina.out
       localhost.log

       By Default the logs files will be empty, once we start the tomcat server log files are genrated and we can see it...,Once u stop the server these wont delete
       
webapps: In webapps Directory we find 5 default webapps, when we deploy war file it is going to deploy here...
         In same tomcat server can we deploy n number of appliations??
         Yes it is possible to deploy all applications in tomcat server
         

work: After deploying those webapplications those apps will generate some files and going to keep in work directory, These files are used 
      While using the application, we dont do any configurations in this directory

temp: temp Directory contains all the temporary files here...

# Tomcat server Installation

If we want to Install tomcat server, is Prerequisit soft is needed??
Yes it is need 

JAVA is needed to install as dependency for this Application 

For tomcat server JRE server is Enough, FOR Maven JDK is Needed..

If we install JDK does tomcat server works???
Yes it work 

But JRE is Mini version just for environement support not for development, hence JRE is enough for Tomcat..

javac -version to check JDK is installed or not if not JRE is there...

# Version compactibility is needed to install Tomcat, Check Documentation which version is to be used....

Tomcat 9.xxx
Java 1.8 or java 8 

Install tomcat server always in Linux server only not in windows

Refer Readme file for Verison compactibilty in tomcat documentation...

Important Port numbers:

SSH -22

FTP -21

HTTP -80

HTTPS -443

SMTP - 25

Mysql - 3306

Follow Mithun Technologies blog as well as TOmcat offical page to download file and modify here and there for installations....

Extarct that zip or tar file which is downloaded, for example if you are in opt directory

Eg: /opt/apache-tomcat-9.0.59

ls the files are visible..

as you have seen above for tomcat directory structure...

.....> Go to bin directory and start the tomcat server
sh startup.sh

Always you need to go to bin directory to startup the tomcat server or give full path like this

sh /opt/apache-tomcat-9.0.50/bin/startup.sh

Before executing, check execute permissions as permissions are not avaialble

chmod u+x *.sh (giving Execute Permissions for all the users in bin directory, shell files * indicates all files .sh means shell script files)

so TO make it easy and access any where in server

Create soft links:

ln -s /opt/apache-tomcat-9.0.53/bin/startup.sh /usr/bin/startTomcat

ln -s /opt/apache-tomcat-9.0.53/bin/shutdown.sh /usr/bin/stopTomcat

Always check path where you have Extracted might be extracted some where also, check and give proper path by using pwd

# To check Process PID of TOmcat
ps -ef | grep tomcat

It will give process id, if it is running...

# How to Access Tomcat, if it has started...

For Every Default application which is already present in web apps folder There will log for every app in logs folder..

If u are Using AWS, Take the server public IP address

If u are in Laptop, Take your laptop Private Ip

http://AWS_public_IP:PORTNUMBER

If we try to access we get an error, By default the tomcat server is running with 8080 
check if any port is already opened in linux server

disable that port or change the tomcat port number or check firewall whether port number is opened or not...

In AWS check Security Groups and Enable Port number or If you are beginner and learnning enable ALL port numbers

ALL_TCP...........8080........Anywhere and save it in AWS server

With out COnfig of AWS Security groups, you cannot access the Web application..

We need to still configure more...

403 Access denied Page is Visible ...

Means The Application is published and still few things left to do...

# Need to configure few things

GO to webapps Directory in Tomcat
ls
cd manager
ls
cd Meta-INF
ls
context.xml
open this file 

nano context.xml

Comment out few lines, find these lines and comment out the section..
<!--
<Valve className>="org.apache.catalina.valves.RemoteAddrValve"
   allow=127\.---------------IP" />
-->
This How you comment the section with 
<!-- 
Lines of code and ends the comment with
-->

Now, if u go back the server and refresh, it works

TO clear Browser page cache CTRL+SHIFT+DELETE button

TO Force refresh the Page CTRL + F5 Button

Just do refresh thats enough 

* Do the same for Host-Manager also, so that you can access Host-manger page as above we just cnfigured Manager Page only in that web app..
  repeat same steps but in Host-manager folder and files which are preseent in same directory..

* if you are using tomcat server in your laptop you no need to comment this as it means to access only locally in that server or laptop only
If you are using AWS server or any other server and accessing through client remotely and want to access tomcat in ur browser you need to comment out these above sections, then only it will work.

# Config the credentials

Go to conf Directory

and Open 

nano tomcat-users.xml

and scroll down and 

add 

<user username="Tomcat" password="password" roles="manager-gui,admin-gui" />

You can create n number of users also like this..

you can create password what ever you like or by Admin choice..

save the file

and login using these details

By giving the Roles Such as 

Manager.gui : we can access server Status and manager App

admin-gui: we can access Host Manger app

This user we have two roles that why we can access all three apps, which are displayed in Tomcat App page,
If we dont provide any one of them those features and access will be disabled..

# Is it possible to Run more than one Service with same port number 
NO...

As if you are using some other application with same port, you will not be have access to tomcat server 
check the port if any other application is occupied 

or change the port number 

Go to /Conf Directory in TOmcat app

there u will find server.xml

nano server.xml

FInd this line where it says port 8080 and edit that from 8080 to 8081 or any other port number like 8082 8083 untill it is not used..

<connector port="8081" -------------->

We cannot specify reserved port numbers 

some of reserved ports are 0-1023 These are already reserved by Operating system..

Always restart the server after configuration of the server

stopTomcat
startTomcat

Edit Portnumber in Browser "IPaddress:8081 and hit Enter"

you will see page of tomcat if that port is not used or if your security groups is configured properly or add rule in it...

networking concepts required to make application works..

# Deploying the Application..

TO Deploy an Application a WAR file of JAVA_APPLICATION should be copy/move/locate in that Webapp folder of Tomcat Application folder.

or

Visit WAR file to deploy section in GUI(graphical User Interface) of tomcat browser and scroll down

click on Browse and click on deploy  

This works if WAR file is in your laptop

# If we want to transfer file from laptop to server or from server to laptop
we use the tool 

winscp
or
ftp commands
or 
filezilla

* How to set password for AWS server
passwd ec2-user
newpassword
re enter

Before we Transfer file from one server to another 

we need Public_IP and ec2-user and password

we have already set password for ec2-user

In AWS When are connecting using Username and Password, we need to do configurations....

we need to enable password Authentication in AWS so that we can communicate.

In filezilla 
we need to give 

Hostname
Username
password
Port: 21 to ftp

and click on connect, it will fail if you dont config in AWS as by default password connection is not supported as we communicate through SSH
Only

Open in AWS Server

nano /etc/ssh/sshd_config

Check for password Authentication and change it to yes and save it...

PasswordAuthentication yes

systemctl restart sshd.service

and check AWS Security Groups also and allow Port=21 as FTP service or enable all ports as Anywhere if you are practicing..

or 

You can use scp command also 

Need to do SSH config using ssh-keygen before we send files to one server to another

Syntax to copy the file from one server to another
scp /var/lib/jenkins/workspace/my_first_jenkins_job/target/*.war root@172.31.90.14:/opt/tomcat8/webapps/

# In JBOSS/ Wildfly

we see deployment folders in these apps for deployment of apps..

# Application context path

http://Public_Server_Ip:PortNo/{context path}

http://Ip_address:Portnumber/maven-web-application

context_path is nothing but application name which maven is creted for war file..

* we can check status in tomcat server whether it is failed or sucess..

This app can be access by any one if it is live in public_ip..

These packages wil be shared with middle ware admins and they are going to deploy the apps manually 

* In real time the Live apps are going to use by Domain names not by Ip address..

* can we deploy more than one application with same context path: NO it wont access as it will get confused which to serve..

* It is not going to allow to deploy more than one app with same context file


# Deploy directory or WAR file located on server

context Path: /Syedapplication
Version
XML Configuration
WAR Directory Path: /tmp/maven-web-application.war

same application with different context path is possible, Just change the name in contect path section

Above we have changed the context path of app and deployed same app again 

We can deploy n number of times of same application but with diferent context path..

* We can stop an Web-Application with in GUI itself by using start or stop buttons..

* we can see how many people are accessing the application..

* Undeploy: Means it is going to remove application from tomcat server..

* It can give session information also which client accessed from what time to what by IP_address..

# Deployment means nothing but copying the war file from One place to another place like web serveer application folder

or It May be from server to server as we have seen above

If the war file is with in server

Go to war file location 
Do pwd and copy the path

Go to location where u like to copy
Enter command

cp /tmp/maven-web-application.war .

here source is path and destination is "." as . represents current directory where i am in to copy from path to paste here..

# Hot Fixes /Hot Deployments

These are nothing but, we are directly going into the servers and updating the server files..
For small changes we go and fix things by going in to the servers

In real time we are not going to do like this, we are going to Automate it..

* If we have updated something in front end we dont need to do reload in tomcat GUI 
* If we have updated something in backenf and we have to reload in tomcat GUI and then only it will work..

* Idle is used to set timeout to log out session and tells to re login again..

# Real Time Deployment using CI/CD Process
 
The Above Ways are not going to deploy in Real Time as we use Automation using Maven, Jenkins, TOmcat and other tools..

No manual Intervention happens..

# Difference between Webservers and Appservers

Appservers:
In App servers we have deployed WAR file and Backend related code.
In App servers it contains Business logic like communicating with databases and we use programming languages such as Java,python
These application contains logic and change from time to time.


Webservers:
Apache HTTP Server
Nginx
IHS - IBM HTTP Server
Oracle I planet

Webservers can server only Static content Only, Front page Information, we cannot deploy backend related code.
The Content which is not going to change are static content such as HTML,css,JS,Images

If we want to develop a website it contains only a website static content and it doesnt contain business logic.

webserver can be used only for load balancing purpose..

The applications are deployed in multiple instances and Webservers are configured as loadbalancers on top of App servers

It is going to follow round robbin algorithm where, every request is distributed in sequence abd return to origin and moves to next..

The setup of Loadbalancing with various servers is also called as Reverse Proxy

where customer doesnt know from which server web is serving the request.

* can we use different Algorithms instead of round robbin, Specifically
It is possible 
By using Weight based 
and 
Sticky session

The Video is Present in Youtube by Mithun Technologies about how it works and Now a days we are not using and AWS has ELB and we are using it for load balancing..

We use this Setup of Nginx Load balancing in Small Companies....If People doesnt Afford to use ELB services..


# How to Install HTTPD server

Yum install httpd -y  (TO Install Htppd Server)

It is going to create a user called as Apache user and it is going to create a service also 

service httpd status (How to check the status)

service httpd.service (To Start a Service)

By deafult Httpd server runs on port number 80

Copy IP Address and port number in browser, you can see sample page of Httpd server test page...

If you see this test page Red hat Enterprse 

we can deploy static content in this directory

/var/www/html/

so here we are going to use the path where we are going to deploy the static content

so Now

go to that above directory, Nothing is here

Create a html files

index.html syed.html 

you can access it in browser by pasting Ipaddress:port and shows index.html page which is created

To access another file like syed.html

Ip_address/syed.html

You will access another html file also ....Apart from index.html if you want to access it you need to give file_name.

You can also access image also ....Apart from index.html if you want to access it you need to give file_name 
ip_address/image.jpg

Check permissions for image before you access as you might get error in page..

* TO Configure Application server URLs for load balancing and other settings like port and path for HTTPd sever, we have httpd.conf file where we do configurations. it is in /etc/httpd/conf directory

Logs will be available in /etc/httpd/conf directory

For More Refer Loadbalancing Ngnix video of Mithun technologies for Load balancing.........

We cannot Run both HTTPD or Nginx server at a time as port number conflict 

change port number and Run it....
.............................................................................................................................................

# Load balancing:

Loadbalancing is a process of Distribustion of load between all servers

We deploy accross all servers to provide high availabilty

High Availability means server should up and running 24/7 In production environments..

we create Multiple Application servers and distribute load accross using webserver by load balancing feature..

HTTPD or Nginx or IBM Http server.... we can acheive load balancing

we have to configure IP address in Nginx server

we have One Nginx server

and more than three application servers...

Install Nginx in One server

and Three or more TOmcat App servers and Deploy Application in all three and up and Running and should be online....

COPY all Three Application tomcat servers Ip_address and port numbers and app names as need to configure in nginx 

Like 

http://ipaddress:portno/application_name(context_path)   application name can be tomcat deployed app name which is configured while packing the java app.


we will be configuring Nginx server on top of the load balancing server, if we get request to Nginx server and these servers the request will be routing to any one these servers and load is balanced

* Install Nginx server in RHEL or Ubuntu or any Linux server

* Ensure to login as root

* systemctl enable nginx.service

* systemctl start nginx.service

# Load balancing with Nginx
http://Ip_address:80

Rename default nginx conf file
sudo mv /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bkp

* Create nginx conf file in default path and define proxy (reverse proxy rules)

* sudo vi /etc/nginx/nginx.conf

events{
    worker connections 1024;
}
http {
  Keepalive_timeout 5;
  upstream tomcatServers {
      keepalive 50;
      server IP_address:portno;
      server IP_address:portno;
      server IP_address:portno;
    }
    server {
       listen 80;
       location / {
            proxy_set_header    x-Real_IP $remote_addr;
            proxy_set_header    x-Forwarded-For $proxy_add_x_forwarded_for;
or;
            proxy_set_header    x-Forwarded-Proto $scheme;
            proxy_set_header    Host $host;
            proxy_pass http://tomcatServers;
        }
    }
}


nginx -t         (To check config file error or syntax issues)

nginx -s reload  (to reload the COnfiguration files)

systemctl restart nginx 

Instead of accessing Application url, USe Nginx Load Balancing Url

Ip_Loadbalanceurl:portno/context_app_name

502 Bad Gateway is error is going to get when SE linux is enabled 
Security Enhance linux is a kernel security module which have linux admins to have more control over the who can access the systems

How to make it work:

setsebool -P httpd_can_network_connect true

Once we execute this command we are going to access nginx url.

WHat is Default Load balancing Method:
Round robbin algo : request passes accross the servers

# if you want to down a server 

GO to nginx.conf file


http {
  Keepalive_timeout 5;
  upstream tomcatServers {
      keepalive 50;
      server IP_address:portno;
      server IP_address:portno;
      server IP_address:portno down;

save it 

systemctl restart nginx 

One server of that Ip is down now..

# How to give preference to a particular server which is high in configurations:

Use Loadbalancing method call as server weights;

GO to nginx.conf file 

Use a parameter called as weight 

assign it to a server IP

http {
  Keepalive_timeout 5;
  upstream tomcatServers {
      keepalive 50;
      server IP_address:portno weight=4;
      server IP_address:portno;
      server IP_address:portno down;

4 request will go to this server, By default One request will go to each server and we have increased weights for server.

save it

systemctl restart nginx

# Backup parameter

When servers are down, then only request goes to backup server

GO to nginx.conf file 

Use a parameter called as backup

assign it to a server IP

http {
  Keepalive_timeout 5;
  upstream tomcatServers {
      keepalive 50;
      server IP_address:portno weight=4;
      server IP_address:portno backup;
      server IP_address:portno down;

save it

systemctl restart nginx

such a system is called Reverse proxy

Why we are calling as Proxy, we have deployed an application to the servers and end user is accessing these applications with the nginx server
we have given nginx server url not the app url

we are hiding the taget Ip address and all the Information, we are proxing the details and nginx server details are visible 

Hence it is called as Reverse Proxy..

............................................................................................................................................


