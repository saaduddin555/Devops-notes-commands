# SoanrQube
Sonarqube is a source code analysis tool

Code Coverage: As a developer he needs to write a code, to test the sourcecode he need to do programmitically what we are doing??
As a a developer he is going to write a test cases to test the source code programitically..

Code coverage is nothing but how many lines code is tested by unit test cases 

A dev has written hello world.java which is having 100 lines of code and also written hello.test.java

so after runnig this one, it has just test 92 lines of code, remaining is not tested, we did not write the code so what is the code coverage..

The percntage is 92%

A/c to industry standards the project code coverage should be 80%

80% of code can be tested by using any test cases

what about 20% ??? 

The selenium automation will cover it...Who is going to write Selenium automation source code, test engineer will write it, tester will do it


Code Review: Code Review is nothing but we are validating the code against the standards whether developer is written source code as per standards or not, so it is very difficult to go line by line like in real time there will be 1000's of source code lines 

How many source code line do your project have???
Its depends on project size and i have worked on various project, one of the project had 40,000 lines of code , 1 lackh lines of code also was there, we can answer same

To do code review static analysis we use sonarqube, it is going to analysis of sourcecode and identify if any issues are there..
If dev is not following standards it will genererate a report and these issues will be fixed by developer

so, sonar qube is not going to identify logical analysis only static code analysis is done here...

some naming conventions and standards..

Who is going to do code review senior developer or technical lead is going to do..

Sonarqube: Continious code quality tool and monitor the code
Vendor is Sonar
Is it opensource.....Some languages only
Verison....9.x
Operating system....cross platform
Extract and use it software

* Sonarqube is previously called as sonar is and open source software quality management tool.
* It will continiously ananlyse and measures quality of the source code.
* it will generate the report if any issues in html format/PDF format
* it is a web based tool and it supports multiple languages (java, C#, JS ..)
* it will support multi os platform also like windows,Mac,Linux
* It will support multiple databases (Mysql, Oracle, Microsoft SQl Server, PostgreSQL)
* supports multiple browsers (Edge,Firefox,chrome,safari)
* It will identify the below category of issues.
  --Duplicate code
  --Coding standards : Follow proper coding standard and usage of functionsthan repeted and proper coding standards and gives suggestions also
  --unit test      : it checks unit test cases which are written by developer
  --complex code   : writing if else satement multiple times more than 3 times and not calling functions makes complex 
  --Comments'      : sonar scan comments and doesnt allow multiple comments unnecesarly, like keeping code as comment.
  --Potential Bugs : it will find potential bugs which are having loop holes in code
  --Architecture and Design : Java has more than 25 Architecture and design patterns which dev need to follow where ever is required.

Maven/TOmcat/ -------> Developed Using Java ------> supports only Java Platform Language
Sonarqube/Nexus/Jenkins----->Developed using the Java ------>Supports Multiple languages 

* Sonarqube has inbuild database called as "H2" if we dont integrate any other database server, it stores data there...

* Sonarqube gives Issues and suggestion to fix the code by giving report..

Initially the sonarqube is used to develop only java projects.....But now it supports more than 20 languages..

Commercial: ABAP,Cfamily(C,C++ and objective C), COBOL, PL/SQL, Visual Basic, Natural, VB.Net, RPG, Swift..

Opensource: JAVA, Java Script, C#, Web(HTML, JSP, JSF,..)XML, Python, Groovy,PHP, Puppet,Lua,Groovy,Fxcorp,Flex,Erlang 

# What are the Pre-requists

To Install Sonarqube, Install java first..
SQ server version 7.8 hence use Java 8 or java 1.8

SQ 7.9, 8.1, 9.x and above use JAVA 11 or java 1.11

Go to Sonardocumentation and check compactibilty and notes

The JRE package is Enough for SOnarqube.

The Sonarqube requires minimun 2gb ram to work...

GO to Official website before installing Any software..

# Sonarqube Architecture..

GitHub_sourcecode.....>Sonarscanner........>Sonarqube_server.........>sonar_compute_Engine.......>h2 or external database.......>webserver.....>search Engine

The code is fetched from SCM repo and we are not going to give packages like war/jar/ear packages to analyse the source code.

sonarqube scanner is going to Analyse and read the code if any issues are there and the report is sent to sonarqube server.

Sonarqube server we have a componenet called as compute Engine and it classifies code into three categories
* Vulnerabilities
* Bugs
* code smells 
And this store in the database, if we have configured external database like oracle,mysql it is going to store over there
or
It stores in inbuild database.

As a developer we want to see the report right, we have a component called as webserver, what ever there is in the database which is store it is displayed in dashboard.

It has search Engine also inbuild which makes to search results very quickly and display in dashboard.

# How to Install Sonarqube Server

##Login as a root user
sudo su -

##Change dir to /opt 
cd /opt
yum install wget -y
wget -c --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u131-b11/d54c1d3a095b4ff2b6607d096fa80163/jdk-8u131-linux-x64.rpm
yum install jdk-8u131-linux-x64.rpm -y

java -version

#Hardware Requirements for SonarQube
#----------------------------------------------------
#The SonarQube server requires at least 2GB of RAM to run efficiently and 1GB of free RAM for the OS.

#Login as a root user.
sudo su -

#Download the SonarqQube Server software.
cd /opt
yum install wget unzip -y
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-7.8.zip
unzip sonarqube-7.8.zip


#As a good security practice, SonarQuber Server is not advised to run sonar service as a root user, so create a new user called nexus and grant sudo access to manage nexus services as follows.
useradd sonar

Give the sudo access to sonar user
visudo

sonar   ALL=(ALL)       NOPASSWD: ALL

Change the owner and group permissions to /opt/sonarqube-7.8/ directory.
chown -R sonar:sonar /opt/sonarqube-7.8/
chmod -R 775 /opt/sonarqube-7.8/
su - sonar
cd /opt/sonarqube-7.8/bin/linux-x86-64/

./sonar.sh start

Troubleshooting
--------------------

sonar service is not starting?

a)make sure you need to change the ownership and group to /opt/sonarqube-7.6/ directory for sonar user.
b)make sure you are trying to start sonar service with sonar user.
c)check java is installed or not using java -version command.

Unable to access SonarQube server URL in browser?

a)make sure port 9000 is opened in security groups - AWS ec2 instance.

Create SonarQube server as a sonar service
--------------------------------------------------------

ln /opt/sonarqube-7.8/bin/linux-x86-64/sonar.sh /etc/init.d/sonar

vi /etc/init.d/sonar

#add below lines in /etc/init.d/sonar

SONAR_HOME=/opt/sonarqube-7.8
PLATFORM=linux-x86-64

WRAPPER_CMD="${SONAR_HOME}/bin/${PLATFORM}/wrapper"
WRAPPER_CONF="${SONAR_HOME}/conf/wrapper.conf"
PIDDIR="/opt/sonarqube-7.8/"

#Enable the sonar service
sudo systemctl enable sonar

#Start the sonar service
sudo systemctl start sonar

#Check the status of the  sonar service
sudo systemctl status sonar

The default username is admin

The default password is admin

* How to disable the Menu access when it is not logged in............>login first

Security...........>............>force user authentication....>Enable it.

Without login you cannot see page

* change password for sonar_server and Myaccount....>security....>change password......>old_pass.......>new_pass.
Remeber the new password as it is difficult to reset it.


* Tomcat/Jboss/Wildfly/jenkins----------->8080

* Nexus/Jfrog artifactory------------>8081

* sonarqube----------------->9000

* MysqlDB...................3306

The default port number is .....9000
The default context path is ...> /

IF we want to change context path, if needed
Go to sonarqube home directory
conf/
sonar.properties

Here in this file we can configure usercredentials,Databases, As default it is H2, Mysql,postgre, and Port and context path also

like below
In webserver section we can change portno and context path

sonar.web.context=/syedtechnologies
sonar.web.port=9000

From now it uses contect path as Ip_or_domain:9000/syedtechnologies as Url if we configure contaxt path

If it is commented using # we need to uncomment it..

GO to sonar.sh lcaotion

and restart after changing the settings and 

sh sonar.sh restart

sh sonar.sh status

When restarted process id changes.

# Executing

we cannot start sonarqube server with root user and we need to create a new user called as sonar and grand sudo acess to manage the sonar services

useradd sonar

nano sudo

sonar ALL=(ALL)  NoPASSWD: ALL

Change the owner and group permissions to /opt/sonarqube-7.8/ directory.
chown -R sonar:sonar /opt/sonarqube-7.8/
chmod -R 775 /opt/sonarqube-7.8/
su - sonar
cd /opt/sonarqube-7.8/bin/linux-x86-64/

./sonar.sh start

and follow installation steps which are above mentioned

sonar.sh status

su - sonar       (switch to sonar)

sudo su -sonar  (sudo access to sonar)

sh sonar.sh start

sh sonar.sh status

When sonar is not running, we need to check log file
go to logs directory sonar.logs

If any issues it is mentioned heree

ce.log   compute engine logs
web.log   webpage logs
sonar.log   sonar server logs
es.log       elastic search.log

Check logs always if you face any issues.....

If the issue is related to temp file
Check temp file which is creted by root user and that file is being used by normal user, hence delete temp files, these will create again when u use again
earlier if you have accessed using root user these issues occur
hence always create a user and perform tasks, mismatch of user config gets errors..

# How to execute sonarQube report for a Java Project
Take the sonarqube server url and username and password

Configure server url and login details in pom.xml file

Go the pom.xml file

In pom.xml we have Tag called as <properties>, here we have to configure sonarqube server details
<properties>
search for sonarUrl and sonar admin and password
<sonar.host.url>http://Ipaddress:portno or domain-name/</sonar.host.url>
<sonar.login>admin</sonar.login>
<sonar.password>admin</sonar.password>
</properties>

* we should not use password in realtime and use tokens instead of password..


What is command to create the build artifact??
mvn package

what is the command to generate sonarqube report
mvn sonar:sonar

mvn (mavenbuildtool) sonar(is going to represent plugin_name):sonar(Goal_name)

If Build is success, Go to sonar_Dashboard and refresh it..

You will see one java project..with or without errors

Who will fix errors??? Devloper will fix the errors.

using username and password is not a good practice in pom.xml as every developer or bad actors can access it..

Use TOKEN instead of password

# how to generate token:
Go to dashboard.......>Username......>admin....myaccount....security........users.......tokens.....generate token......copyToken
Go to pom.xml and 
remove password and username also
Instead of loginid and Password, Just use token

<sonar.host.url>http://Ipaddress:portno or domain-name/</sonar.host.url>
<sonar.login>paste_token_here</sonar.login>

Remove password section
and save it..
Execute sonarQube report it will work.

* Most of time build will fail with error sonarqube server cannot be reached..
Check the IP and domain name or sonarqube Url which is given is correct
check pom.xml configurations.
or check public or private ip
check port no
check firewall or security group
check Authentication
check internet connectivity

# App Scan:(This was IBM product earlier no it owns by HCL)

This is one of the popular tool of Vulnerability checking
Using this appscan we can generate reports for any programming languages like Python,Javascript,node.js
It is not open source and it checks Vulnerabilities 
It check any loopholes and hacking, sniffing, tools
Ecoomerce and Baking apps does Vulnerability,security,penetration testing, if there are any issue they denfity and deploy the code
These Things we gonna learn in DEVSECOPS

Dev and security is DevSecOps

Only one or two security tools is enought to become DevSecOps.
if there are loopholes hacker may access the application and need to change something in it 

sonarqube is different and Appscan is different.

# node.js Project sonarQube Execution.
Check any node.js project and clone it to any linux server
to run report execute command:
npm run sonar
TO execute npm command you need to install node.js software

yum install nodejs -y
yum install npm -y

To use windows or other os use google or node.js documentation to install

Like pom.xml in java we have sonar-project-js file in node.js
there we need to configure sonar server Url.
and 
sonar.login=token

and run commands and execute and generate the sonarqube report.

# code smell in sonarqube dashboard helps to identify code issue 
Which java file
which line of code there is issues.
It gives suggestions to replace also.
and dev can fix the issues easily.

If Dev want to check report, We need to just share sonar server Url and Credentials, he will check the report

SonarQube can also generate report in PDF format also for that we need install few plugins to do that...


# Sonar Dashboard

In sonardashboard on right hand side we see How many CODE LINES like 20k 30k etc etc and give code type like XML,java,JSP automatically it will identify by file extensions which is given while ceating source code, below the last analysis date and time 

* if you see Code coverage as "0" in dashboard of the project it means there are no Unit test cases written for that Project.

* if you see Duplication as "0" in dashboard of the project, it means there is no duplication of lines in the code.


# Tabs

* Projects Tab: It is going to show all projects which is executed

* Issues tab: It is going to show all projects issues at one place

* Rules tab: In rules tab we see alll rules related to project such as which are predefined rules and checks the code accordingly

FOr 

Languages:

JAVA: 537 rules

Pyhton: 439 rules

c#: 367 rules

Javascript: 216 rules

PHP: 181 rules

Each language has its own rule set and scans the code and generte the report to follow the rule set..

we see all the details in rules dashboard.


* Quality Profiles: Collection of rules which we are going to apply when doing Analysis.

we rules like 537 rules for java

if we dont want to apply all rules for the project and do some selective analysis and rules to project that time we use Quality profiles. 

Some project they use 10 rules or 30 rules 

As DevOps ENgineer we need to create Quality profiles based up on developement team requirment.

* How to create a quality profile for each language there is one qulaity profile.
  Java 1 profile----381 rules----settings---updated......

  To create custom quality profile
  click on create
  New Profile Name: facebook
  Language: Java
  Parent: None

  create

  To add rules click on profile which is create and click on activate more.

Just click on Activate button on right hand side which is necessary and save it.

Sonar-way profile is default profile_name for all project

can we make default for custom quality profile

Yes
 
click on default button or click on settings symbol and select options..default and Sonarqube takes Quality profile as default for all project executions.

* custom quality profile for single projectof lang not as default to every project 

- Click on project
           overview   issues   Measusres  code    activity   Administration

- Go to Adminstration
- If Java Project, select JAVA and click on custom profile which u have created earlier
- Java quality profile is sucessfully updted

As per Quality profile rules it will validate the code. Not all the rules.

* Quality gates

Quality gates is collection of conditions which we are going to apply while executing the sonarqube report like 

Quality Gate passed

Quality Gate Failed

We are giving Metric such as 
Coverage on New code                             is less than 80% eroor
Duplicate lines of code                          is gretaer than 3%
Maintainability rting on new code                is wore than A
Reliability rating on new code                   is worse than A
Security rating on New code                      is worse than A

If these qulaity gates criteria is not met the build will fail

By Default soanr-way is default quality gate

It will exectue the sonar gates for new code not for Old code which is updated 

* I want to do it from begininning not only for new code
How to create our own quality gates

Quality gates.....>Create ........>Give Quality gate.......> facebbokqualitygate.

Click on Add condition

and can add ennumber of conditions here

* how to apply it in project

- Click on project
           overview   issues   Measusres  code    activity   Administration

- Go to Adminstration

- Quality gates

- Choose the custom quality gate

The project may mark as fail if covergae is not met as per quality gates.

* Administration Tab

Administration

                Configuration    Settings     Projects     System    Marketplace

* Configuration consist of all General configuration settings such as

File suffixes and extentions...........TO update config how we want

Jacoco reports of Unit test cases

* settings consist of creating Users and add new users apart from ADMIN and can share details accross developers
  In sub we cannot see admin access as default 
  In admin we need to give previlages to be admin
  
  The sub users will be in Sonar-users group

  For admin access we need to add sub user to sonar-administartor group in settings, Using Admin console we can give access.

  For Any user we can create N Number of tokens for same user and Any user but we need to be root user/Admin user.

* Projects
 We can delete the projects if we are using it using project management section

* System 
It is going to display all info related to sonarqube server
we can restart the server
we can download logs
we can download System Information
We can change log levels
We can see sonarqube home directory
We can see sonarqube Data directory
We can see sonarqube Temp directory

Database Information, Bydefault it will be "H2"
Url, driver, driver version and more

Others such as 

We can check info related to
System
web
computeEngine
Search Engine

# we can configure External Databases also to Sonarqube server

Login to Linux server where sonarqube is installed

We execute these commands to increase Elastic search 

systemctl vm.max_map_count
systemctl fs.file-max
ulimit -n
ulimit -u

Create database and User in postgre SQL as follows:

systemctl status postgresql-11     (TO check status of postgresql)

If not insatlled install postgresql and create a user with postgres

useradd postgres            (TO add a new user with name)

su - postgres              (To switch to postgres user)

psql                        (to connect to postres console)

create database mithuntechnodb;                                              (To create a database with name)

create user sonarqubeuser with encypted password 'password';                  (create user and password for database)

grant all privilages on database mithuntechnodb to sonarqubeuser;            (Exactly give details such as database name and username)


we need to Intergrate the database details to sonarqube server:

conf/
sonar.properties
---------------------------------

#The schema must be created first
sonar.jdbc.username=sonaruser
sonar.jdbc.password=password

In postgreSQl section: You will find

#sonar.jdbc.url=jdbc:postgresql://localhost/sonarqube?currentSchema=my_schema
sonar.jdbc.url=jdbc:postgresql://localhost/givedatabasenameheredb

Why giving local host because both are configured in same server if they are in different servers???

Here we need to give postrgres_database_ip_address_where it is running instead of local host.

sonar.web.host=0.0.0.0

Uncomment the lines by removing # symbols as per these lines.

same file we need to chamge port numbers also 

got to bin/linux-x86-64/   or if manually placed go to sonar home directory where bin is there and execute the command

sh sonar.sh restart

as we have did the configurations, restart is needed.

If the configuration dont change in UI system or any errors.

go to logs folder and sonar.log

to enable debug level instead of info level in logs
go to 
/Conf/sonar.properties

search for /debug in file

#sonar.log.level=INFO

change this to 

sonar.log.level=DEBUG

check logs and troubleshot the error as per log.

* DBclient
To connect to databases using laptops

https://www.sql-workbench.eu/downloads.HTML

install mysql by downloading from this link

Generic package for all systems package download 

Extract it

if usisng windows click on sqlworkbench.exe

and configure serverip and port, username and password and Test connections

and start playing with database, if reports are generated you can see in database or sonar dashboard also

Tools....>db tree......>users.......>copy script and click on play butoon......you will see databases of sonar.


* Marketplace
We can see Various Plugins and Editions of Sonarqube like 
Developer edition
Enterprise edition
Data center edition

.........................................................................................................................................................................


