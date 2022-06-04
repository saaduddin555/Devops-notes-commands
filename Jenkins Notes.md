Instalation jenkins on Ubuntu server:

----sudo apt-get update
----sudo apt-get install maven
--check the version of the java enter the below command:
	 java --version
-- install the jenkins on Ubuntu server please enter the command as mentiones in bracket
  [   curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins ]

---- get the key from the below bath and past in the jenkins website:

cat /var/lib/jenkins/secrets/initialAdminPassword

-- registered a jenkins admin--
---- install the sugusted plugins--
Now you are succuesfull installd the Jenkins


------------------------------------------
create the Key gen for jenkins user
-----------------------------
---- sudo -s   (switch as root user)
--- su - jenkins (Switch to jenkins user)
----ssh-keygen   (creating the keys)
---cd .ssh
---- cat id_rsa.pub (copy that public key)


---------------------------
Tomcat installation
--------------------
 --- sudo apt-get update
----- sudo apt-get install maven (install java)
--- cd /opt
 ----  sudo wget https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.73/bin/apache-tomcat-8.5.73.tar.gz
        (get the apache tomcat package)
----- sudo tar xzf apache-tomcat-8.5.73.tar.gz   (unzip the packages)
----- sudo mv apache-tomcat-8.5.73  tomcat8
-----  echo "export CATALINA_HOME="/opt/tomcat8"" >> ~/.bashrc
----- source ~/.bashrc
---   cd /tomcat8  (go inside the tomcat8 directory)
---  sudo ./bin/startup.sh  (start the tomcat server)
---- http://ip:8080        (check the tomcat with the ip and 8080 default port number)
------- cd /opt/tomcat8/conf 
----- nano tomcat-users.xml (add the below user into that file)


 <role rolename="manager-gui"/>
  <user username="tomcat" password="s3cret" roles="manager-gui,manager-script,manager-jmx,manager-status"/>
----- cd /opt/tomcat8/webapps/manager/META-INF
------ nano context.xml
------ comment that <valve section as below
<!--  <Valve className="org.apache.catalina.valves.RemoteAddrValve"
         allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />
  <Manager sessionAttributeValueClassNameFilter="java\.lang\.(?:Boolean|Integer|Long|Number|String)|org\.apache\.catalina\.filters\.CsrfPreventionFilter\$LruCache(?:\$1)?|java\.util\.(?:Linked)?HashMap"/> -->
--- cd /opt/tomcat8/bin/
--- ./shutdown.sh 
---- ./startup.sh


--------------------------------------------------------------------
make ssh connection between jenkins and Tomcat server
--------------------------------------------------------------------
--- sudo -s (switch to root user)
---- ls -al
--- cd .ssh
---ls (there you can find the authorized_key file)
---- nano authorized_key
--- past the key which you copied from the Jenkins public key---
-----------------------------------------------------------------
IF YOU WANT TO TEST THE CONNECTION YOU CAN DO SSH FROM THE JENKINS SERVER
BUT YOU SHOULD BE AS JENKINS USER IN JENKINS SERVER)
----- ssh root@privateip of tomcat


Syntax to copy the file from one server to another
-- scp /var/lib/jenkins/workspace/my_first_jenkins_job/target/*.war root@172.31.90.14:/opt/tomcat8/webapps/
............................................................................................................

# Jenkins 

Jenkins is an opensource Java based CI tool

2004 They have released first version called as HUDSON

In 2012 they have started Jenkins Community

What is continious Integration:

Continious Integration is the process of Automating the build and testing the code everytime when a developer pushes the code to version control system

If you want to implement continious integration what are the tools you are going to recommend ???

Github
Apache Maven
Sonatype Nexus
SonarQube
Jenkins
Apache Tomcat


Suppose if it is .NET Application can we implement CI/CD??
 Yes we can do , it can work for multiple languages 

we have to change the build tool for other languges..
MS build is tool we will us for .NET

Suppose If we did not integrate CI/CD Model, What will happen?

All the build process will be done manually and delay of process and delay of fixing issues and should be dependent for each other task

                         CI/CD Jenkins
DEvelopers......Github......Maven Build......Sonarqube......Nexus..........The Package is tested and deployed TO, App server like Tomcat.......Send an Email Notification

Immediate Bug detection is main advantage of using Jenkins

If Any Issues in build, the build will fail and Project history of build also is recorded in jenkins Server..

# Build will Fail:

If dependencies are not there or wrong configurations or not available in Repository

Developer did not test code properly and pushed the code or compilation error

Sonarqube server is not up and running or issues in code quality 

Many reasons ....

# Continious Delivery

CodeDOne------Unit Test----Integrate----Accept test----(Manual)----Deploy to production(we do here Manually to deploy to production)

# Continious Deployment

CodeDOne------Unit Test----Integrate----Accept test---(Automatic)---Deploy to production   (It deploys Automatically deploy to production)


# Environments:

Dev Env

QA ENV

Pre-prod

Production

Continious Delivery we are going to implement for External projects.    Like Clients Projects.., we need to take Approval from client.

Continious Deployment we are going to implement for Internal Projects/ In House Pojects.  Like HRMS tools or internal tools.

The Testing team will write Automation test cases like Selenium, Once it is passed we are going to deploy other Environment..

# What Jenkins can do 

Integrate with many Different Version Control Systems such as Github, Gitlab, Bitbucket et
Generrate Test Reports such as JUNIT
Push the builds to various artifacts repositories
Deployes directly to production or test environemnts
Notify to stake holders of build status through email..


# Benefits of Jenkins
It’s an open source tool with great community support.
Easy to install and It has a simple configuration through a web-based GUI, which speeds up the Job
It has around 1500+ plugins to ease your work. If a plugin does not exist, just code it up and share with the community (https://plugins.jenkins.io/).
Its built with Java and hence, it is portable on all major platforms. 
Good documentation and enriched support articles/information available on internet which 
will help beginners to start easy. 
Specifically, for a test only project, it is used to schedule jobs for regression testing without 
manual intervention and hence monitor infrastructural and functional health of a application. 
It can be used like a scheduler for integration testing and also can be used to validate new 
deployments/environments on a single click on a Build now button.

List of popular Continuous Integration tools
SNo Product Is Open Source?
1 Jenkins Yes                  (This is Compunity Edition) Free
2 Cloudbees Jenkins No         (It is a ENterprise Edition), Facing any issue u get support from team, paid service
2 Bamboo No                    (Atlassian is Vendor.) like JIRA, BITBUCKET are Atlassian compnay tools they are paid 
3 Cruise Control Yes           
4 Travis CI Yes and Paid also
5 Circle CI Yes and Paid also
6 GitLab CI Yes and Paid
7 TeamCity Yes and Paid


If any issues Jenkins tool, Community developers will fix the issue by raisig the Jira ticket, its not chargeable, its free and JIRA tool is maintained by Jenkins 
community


Jenkins can be used by any IT professionals also 

Like Test Enginner uses to test thier test cases and creting a job and config repo with git hub and run selenium test cases

Even Db guys write sql queries and Automaate using jenkins like in dev env and qa env 

Instead of writing db queries manually they are Automating using Jenkins

Not only devops dev qa data engineers are using alot

It is used to do Automation


# Jenkins Insatllation requirements

Minimum 4 Gb is required to Run Jenkins as if we are Integrating Various plugins and Build and compile task takes lots of Compute power
For practice we can use 1 gb server..
In real time the server configuration will be more than 8gb server with Master and slave nodes.

Jenkins Installation in Ubuntu Linux Server
 

wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -

sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'

sudo apt-get update

sudo apt-get install jenkins

systemctl enable jenkins

systemctl start jenkins

systemctl status jenkins


# RHEL

java -version

yum install wget -y

yum install jenkins -y


Login as a root user
sudo su -

Install Jenkins

cd /opt/

wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo

sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key

yum install jenkins -y

Enable and start the jenkins service

systemctl enable jenkins

systemctl start jenkins



# Create the project/job in Jenkins
Step 1: Login into the Jenkins, go to the Jenkins dashboard left side top corner, click on New Item.

Step 2: Enter the project name in Enter an item name input box and select the Freestyle project
and click on OK Button.

Freestyle project: This is the central feature of Jenkins. Jenkins will build your project combining 
any SCM and any build system. 
A Free-Style project is a project that can incorporate almost any type of build. The Free-Style project 
is the more "generic" form of a project. You can execute shell/dos scripts, invoke ant, and a lot more. 
Majority of the plugins are written to use the free-style project.

Maven project: A maven project is a project that will analyze the pom.xml file in greater detail and 
produce a project that's geared towards the targets that are invoked. The maven project is smart 
enough to incorporate build targets like the javadoc or test targets and automatically setup the 
reports for those targets.

Multi-configuration project: The “multiconfiguration project” (also referred to as a “matrix project”) 
lets you run the same build job in many different configurations. This powerful feature can be useful 
for testing an application in many different environments, with different databases, or even on 
different build machines. We will be looking at how to configure multiconfiguration build jobs later on 
in the book.

Monitor an external job: The “Monitor an external job” build job lets you keep an eye on noninteractive processes, such as cron jobs.


# Plugins

Plugins are Important Part of Jenkins, when we configure jenkins we install suggested plugins at inital and those plugins will showcase 

* Git: When we would like to connect to jenkins to git server 

 WE to need to install git in jenkins server                         yum install git -y

 we need to check git plugin is installed or not in Jenkins config section in UI of Jenkins.

If we dont install git in jenkins server we get error failed to connect to git hub server as git helps to navigated by using inbuild commands.

If it is a private repo need to add credentials to Jenkins and if it is a public we need not to provide any credentials.

add creentials in credential manageer and configure it in.....source code  management section


# Invoke top level maven targets:
to invoke maven commands 
No need to specify mvn clean package
Just 
clean package is enought

click on build now..


If we get any erorr mvn command error in build failure log, we need to check maven is installed or not in jenkins server

# If a Job is using different maven config verisons

3.8.1

3.8.4

3.8.8 

Every job uses differnt version for that 

global tool configuration in settings and click on MAVEN and give name and details like verison and click on install automatically

and save it.

we change change n number of maven versions in Global config tool.

* In build section instead of default click on select version and build the job...

* The maven dependencies will be downloaded as mentioned in pom.xml file 

# Where build Package is stored in jenkins

/var/lib/jenkins/workspace/APP_NAME_which is BUILD/target/Maven-web-app.war

Jenkins Default Home Directory is 

/var/lib/jenkins----------This is Jenkins Default Home directory

Inside of Home Directory 

we have 

/workspace
 /JoB_name
  /taget
   /web-app.war


# How to get a sonarqube report

we need to configure sonarqube details in pom.xml file which is in Source code Application

Always update sonarqube details which branch u want to use in jenkins.

It will not work if u update some other branches and expect results...

in pom.xml 

we have  sections such as 

sonar.host.url
sonar.login
sonar.pass

edit these sections in pom.xml and save the file 

Instead of username and password we can use token by generating in sonar qube server

and save and commit changes in git hub

Jenkins UI

In GOALS Section we can give

* (clean package sonar:sonar)
   If we want to run only sonar goal run (sonar:sonar)

save and click on Build Now

Build numbers will increament as long u update the project and run jobs in jenkins and keeps track recod in logs

# Upload the artifact in to Nexus Artifact repositoy..

Click on repository details in Nexus and copy the URL of Snapshot and release, if both if u want to configure.

In pom.xml we are going to configure

edit pom.xml 

<repository> section

find 

<name> Syed Technologies Releases Nexus</name>
<url>http://paste the link of releases here which u copied from nexus server</url>
</repository>

<snapshotRepository>
Do same for here also as we did above, Urls get it from sonarqube server
</snapshotRepsoitory>


save and commit the changes

* Configure Nexus Credentials
settings.xml file, where is it located??

The Settings.xml file is related to Maven and hence the Maven is installed in jenkins server
If jenkins UI installed maven we need to go to
go to Jenkins Home Directory i.e is /var/lib/jenkins

In that home directory there is directory called as tools

there we can see MAVEN software

Any software if we Install from Jenkins UI, Gobal tool Configuration method that toool is present in Jenkins/Tools Directory..

If we configure in Jenkins UI and if we dont use that software or version in build process, The tool wont be created in jenkinshome/tools

we need to use once either software or that specific version of tools then only that folder will be visible...

Go to that Maven folder version which u configured in that build job

Find settings.xmml in conf directory

tools/maven_versionno/conf/settings.xml

open the settings.xml and edit the file 

Go to Servers section
<server>
-------
------
------
--------

<server>
<id>nexus</id>
<username>admin</username>
<password>Password</password>
</server>

</servers>

Mention these lines with username and password and save the file 

Now Nexus should run

Configure in Build Goal:

clean package sonar:sonar deploy         (This line will pass multiple goals) such as clean of maven and package and soanr report and deploy to nexus

and Build the Job, 

you can see the Artifact copied to Nexus server


# Deploy Application to Tomcat server

TOmcat sever should be up and Running 

Copy Tomcat server URL

Install Plugin in Jenkins "DEPLOY to CONTAINER"

Without installing this plugin you cannot configure tomcat server details in Jenkins

For this you need to go to Jenkins and go to Plugin Manger and search in "Available" section and install the plugin

click on Install without restart

go back to dashboard

click on job........>configure.........>post build actions

* POST BUILD ACTIONS
  Post Build Actions is Such after Build is Success if we want to pass more arguments like deployment to other containers or get an email notification or many more 
  we can use such actions

You will find Deploy to container option in POST Build Section in Jenkins

select the plugin...


Deploy WAR/EAR to a Container

"The Jenkins By default refers Path till Jenkins WOrkspace Directory"

The WAR FILE PATH IN JENKINS SERVER WHICH IS BUILD

/var/lib/jenkins     -----This is home directory
 
/var/lib/jenkins/workspace    -------This is Identification directory where it sees any WAR files are there

/var/lib/jenkins/workspace/App_dev/target/web-App.war

But 

Our File is After two steps after workspace directory 

hence to give path for WAR file Just give 

** means to skip two directory and search

**/web-App.war   (give this in war/ear location)

* contextpath

we can deploy this war file in any server such as tomcat, JBOSS etc

give tomcat credentials using Add button

username
password

Description: Tomcat credentials 

click on ADD
 
drop down the credential and select and save 

and Build Now

The Buils is Triggered and the deploy into tomcat server

* Errors if we get 403 error, it is forbidden so username what we have given is forbideen to deploy
hence we need to configure the tomcat permissions 

Go to tomcat server

cd opt/apache-tomcat-9.0.59/conf/

nano tomcat-users.xml

scroll down

<user username="name_of_user if it already exist leave it or add or change" password="password" roles="manager-gui,admin-gui,manager-script" />

save it 

How to identify, always use some technical brain or search in google by searching error or issue from jenkins log which is performing action, search and get result
Apply.

Build Now

It will get deployed sucessfully

# How to Automate the Whole Process without clicking build now, BuildTrigger Process

As soon as devloper Pushes the code,it has to trigger the job

we can use three ways

* Poll scm
* Build periodically
* github webhook

* Poll scm: Go to Job, click on config, scroll down, Build triggers, Poll Scm 

Schedule Time

* * * * * Every Minute and save it

Give Cron Jobs Format

What ever the TIme Interval we have configured, That Time Interval Jenkins will go to github and check whether updated code is there or not...
How Jenkins will Identify it whether Updated code is there or not??
It is based on code commit Id 
when we push the code to github , it generated commit id and same commit id is sourced by jenkins and hence it differenciates the updates

If you go to job, Any build no is going to fetch commit id and it is going to compare both and if any changes, the build triggers if any difference...

It checks last commit Id in github, If both commit id is different triggers the job

who Triggered to Know:

SCM change Build has triggered  (Automation triggered which we see in log)

The Build is triggered by user  (Manual trigger in log)

* Build Periodically

What ever the time interval we have given, that time interval it is going to check in repository, Even though there is no updates, Still Build will Trigger

Schedule

* * * * *(No spaces after 5 stars)

STARTED BY TIMER is going to See in LOG



* What is difference between PollSCm and Build trigger

What ever the TIme Interval we have configured, That Time Interval Jenkins will go to github and check whether updated code is there or not, if any update is there it will trigger the build, if not it wont trigger.

vs

What ever the time interval we have given, that time interval it is going to check in repository, Even though there is no updates, Still Build will Trigger


* Github WEBHOOK

We Need to HAVE Admin Access in GITHUB to do the chnages for github webhook configuration

Instead of Jenkins Go and check in github
Whycant 
Github tell to Jenkins that there is update in code

As Here it is not related about EGO, Its About Jenkins will use more Server Resource here to check and hence to reduce in REAL TIME we use Git web hook

Go to Build Trigger Section and Enable the checkBox

-Github web hook in Build trigger section in Jenkins
-Go TO Github and Settings.....>Webhooks

Webhooks allow external service to be notified when certain events happen. When the specified events happen, we will send a POSt request to each URLs you provide

we need to give Jenkins URL and with Context Name

http://IPaddress:portno/github-webhook/

Context type: application/json

secret: leave empty

Which events you would like to trigger

Just push the Event
Send me Everything
Let me select individual events

You can click Individual Events and TIck the neccessary Events

save it 

If you see green colour tick mark after saving, it is going to work

GO to Jenkins, If Dev updates, Jenkins Triggers Automatically....

we can click job and check who triggered build "started by github push by Dev" such message type we would see here...


# How many Jobs are going to run in Jenkins by default.

At a time by default only two jobs are going to Run, if you want to increase we can configure it..

we can configure and increase BUILD EXECUTOR BY 

Click on Build executor Status

Built in Node.....>Configure......>Number of Executors......change the Number and .......save it

# General

Discard Old Builds   
  Days to keep the Build               It keeps last 5days of Build may be 0 if not triggered May be 20 if triggered alot
  Max no of Build to keep              we can give how many build to keep like 5, 10 whether failed or success it will keep that record
  Days to Keep Artifact                we should give same as no of build to keep
Diable Project                        (To Disable the Project by TIck or Untick)


# source code Management

git
null

# Build Enviroment 

Delete Work space before Build Starts        It deleted Old Builds or old ource code for particular project it downloaded it deletes it.
Add Timestamps to the console Output         It add time stamps to console log


# Build 



# Post Build Actions
Aggregate downstream test reults
Archive the Artifact
Build Other Projects
Publish Junit Test result Report
Record JAcoco Coverage Report  
Git Publisher
Email Notification
Editable Email Notification
Set Github commit status
set Build Status on github commit
Delete Workspace when build is Done


# When and how to Diable Project
If we have server issues and If something Dependencies are in Maintainance such as other dependencies servers, if any updates patches should be done
That time we can disable the project or if required we can perform this action..

We can Disable the Project from

Click on Project name on Dashboard.....CLick on Diable Project on Right Hand Side.....

Once you disable the job, Build Now Option will get disappered..

Click on Enable to Enable it Again..

The Build SCM and webhook or Polling doesnt work......

# Jacoco Plugin (java Code coverage)

Install Jacoco Plugin first

Post build Actions

Record Jacoco Covergae Report

Give Values of Code COverage, It should be minimun 80% if the code coverage is not 80% The Deployment wont happen

Enable: Change Build Status According to defined Thresholds

Enable: Fail the build if coverage degrades more than the delta Thresholds

Give 80% or more depends up on Dev call

These Check Boxes should enable to mark as failure and stop the build process, if not it will build it 

To Run Jacoco The Test cases should be written by Devloper, If test cases are not there in Source code repository or not written by dev
The Build will be 0% By default and build fails..

Click on Job and click on covergae Report to see the details

How many packages are there how many Java classes are there...

If there are no Unit test cases written No code coverage is checked..

This Jacoco plugin is going to work only for the Java Projects Only

# How to Create a New Project from Existing Project in Jenkins

Click on New Item

Enter a Item Name

Type of Project : DOnt select any one of the list Just scroll down

See there COPY FROM option 

copy from: facebook-dev   (Already existing project name)

All configurations are Copied from that previosu Job
 
save it

Note: If u clone a project and change Branch Type, U need to configure Sonarqube server, Nexus server also as we are not deploying there, and give proper details.

# Jenkins Directory Structure

/var/lib/Jenkins is Default Jenkins Home Directory

Jobs directory: All Build Information and Jobs related Info is present in this directory.
     The Job names which we have given in Jenkins those job names directory information is available here, may be 5 ....to 1000...n number
     Under Each directory you will see next-Build Number file.
     Build_Dir: It Contains One more directory caled as Build     
          1,2,3,4, This Directory contains Build numbers of Jenkins, each build you will find those many directories
                Each build Number directory you will find Logs, The console output in Jenkins what u see is getting from this directory
                Config.xml: Job Configurations Contains here in this file, Each job contains config.xml
                Change.log.xml contains Changes information

Workspace: This Directory it contains Source code details and Files....
     For Each Job it contains Two DIrectory One is Temp_name and Job_name, what ever is going to download from github repository it is going to download and keep it 
     All Source code is present in this directory
       Under Job_name Directory, we have TARGET directory where war/jar/ear file is Kept.

Tools Directory: Contains What every ever the software configurations we did in Jenkins

Users Directory: We see Users.xml file
                  All the Users Information is Available in Users.xml, The Data is stored in XML Format
                     each users it contains a entry
                     <entry>
                     --------user1------
                     ----------
                     ------
                     </entry>

                     <entry>
                     ------user2----
                     -------------
                     -------------
                     </entry>

Plugins Directory: It contains all the Plugins which we installed in jenkins
                        All the Plugin dependencies is seen in the file
                        The plugin extension will be plugin.jpi

Updates: Contains what ever the updates which are available and ready to install those updates are going to store in updates directory.

logs Directory:
Note: When Jenkins is not working and facing some issue we need to go to this directory path /var/logs/jenkins/jenkins.log


# Create a CI/CD for JAVA APP using Maven Project..

If we Install Pugin Maven Integration we can able to see MAVEN Project in Create New project Section..

What is the difference between Freestyle project and Maven Project

We can create a project for Any programming language using Freestyle Project

We can create a project for java project which has Maven as a build tool is Maven Project

What is the Use of Maven Project:

This Project is Dedicatedly created for java Project which is having Maven as a Build tool.

If we want to use Maven Project we need to configure and Install Maven first in jenkins server

In Build Section:

Select Maven version and Start Building the Project, give git hub Url and do settings as we did above projects

goals: clean package

Extra steps seen in Maven Project:

Post steps:

RUn only if build is success
Run only if build is succeed or unstabel
Run regardless of build result   (select this and save and run)

# Plugin Management

* Deploy to Container                  This plugin takes a war/ear file and deploys that to a running remote application server at the end of a build
* Deploy to Web Logic                  This plugin deploys any artifacts built on Jenkins to a weblogic target (managed server, cluster) as an application
* Websphere Deployer                   Deployment to a running remote or local instance of WebSphere Liberty Edition
* WildFLy deployer                     This plugin takes a war/ear file and deploys that to a running remote application server to Wildfy or JBoss EAP server group


* Maven Integration 

This plugin provides an advanced integration for Maven 2/3 projects.

Even if Jenkins provides natively a Maven builder to use a build step in classical Jenkins jobs (freestyle, ...) this plugin provides a more advanced integration with specific a specific job type providing uniq features like:

Automatic configuration of reporting plugins (Junit, Findbugs, ...)
Automatic triggering across jobs based on SNAPSHOTs published/consumed
Incremental build - only build changed modules
Build modules in parallel on multiple executors/nodes
Post build deployment of binaries only if the project succeeded and all tests passed


* Safe restart                     This plugin allows you to restart Jenkins safely: it's waiting that all builds in progress finished before launching restart.


* Next Build Number

This is a simple plugin that changes the next build number Jenkins will use for a job.
This plugin is typically useful if you are using $BUILD_NUMBER as part of a version string, and:

You do a build outside of Jenkins and you want to skip that number for the next build to avoid duplicate version numbers or failures.
You created a new job to handle an existing process and want it to continue from where the old one left off.
Jenkins requires that build numbers are not duplicated. When you click on the link installed by this plugin, a text field will be shown that contains the next build number to be used. You can change this number to be anything larger than the value for the most recent build

* Jacoco          The JaCoCo Maven plug-in provides the JaCoCo runtime agent to your tests and allows basic report creation.

* SSH Agent

This plugin allows you to provide SSH credentials to builds via a ssh-agent in Jenkins.

This is convenient in some cases. Alternately, you can use the generic withCredentials step to bind an SSH private key to a temporary file and then pass that to commands that require it, for example using the -i option to ssh or scp.


* Email Extension
* SonarQube Scanner
* Audit Trail
* Job config History
* Schedule Build 
* Blue Ocean
* Publish Over SSH
* Thin Backup
* Build Name Setter
• Convert To Pipeline 
• JobConfigHistory
• Repository browser
• Role-based Authorization Strategy: 
• Slack Notification Plugin: 
• Cobertura Plugin: In UI we will see as Coverage Trend.
• Hudson global-build-stats plugin: 
• Delivery Pipeline View: 
• Enable project-based security

Install Plugin using Jenkins CLI.

java -jar jenkins-cli.jar -s http://52.66.245.44:8080/ -auth mithuntechnologies:passw0rd install-plugin 
http://updates.jenkins-ci.org/download/plugins/audit-log/1.0/audit-log.hpi

Search in google for More info related to plugins or click on plugin ingo in Jenkins to know usage....

# Pipeline as a Project...

* Scripted Way
The Pipeline of a Project can be Witten in two ways One is Scripted way and Another is Declarative way

The Pipeline as a Script is using Groovy Syntax

The Pipline Scripts starts with node flower bracket and ends with close flower bracket

The Node here represent where the script is going to run

By default it is going to run in master Instance or node...

Do we need to specify node name....If you specify or if u dont specify it is going to run in master instance itself.

node{

}

* If you want to specify Explicitly node Name you need to specify like this below

node('master'){
stage('CheckoutCode'){

}
}//Node Closing

If you want to run a pipeline as a script you need to select pipeline as a script project..
------------

* Generate pipeline script from snippet generator where ever neccessary...


node{

def mavenHome = tool name: "maven3.8.5"

//checkout stage
stage('CheckoutCode'){
git branch 'development', credential id----------This can be generated using snippet
}
//Build stage
stage('Build'){
sh "$mavenHome/bin/mvn clean package"
}

}//Node Closing


-------------------
By default groovy script cannot fetch global configuration jenkins Installed path, if we just give command mvn clean package it will not work

As we did not install maven in server directly as we installed maven in global configuration section in jenkins server UI

hence we declare a variable of mavenHome path as it is already configured..

In groovy script def is a keyword to create a variable/function

mavenHome is identified by jenkins as it is configured there in GUI when we installed global settings in Jenkins and mvn command to work we need to give path afer maven home as automatically can not fetch it

The path is recognised till mavenHome, and limit to that boundary and mvn command file is present in bin folder to work that is why we are giving as 

$mavenHome/bin/commandname

as mvn package is in bin folder as bin is unreachable to home path, hence we are specifying manually so that script can understand...



* If we dont specify any branch name in git script it will take it as master branch as default...

stage('CheckoutCode'){
git branch 'development', credential id----------This can be generated using snippet
}

Global Variable : A variable which is created in node level is global variable
Local Variable : Which is created in stage level and works with in that stage is local varibale.

Global variable:

node{

def mavenHome = tool name: "maven3.8.5"

//Build stage
stage('Build'){
sh "$mavenHome/bin/mvn clean package"
}
..............................................
Local Variable:

//Build stage
stage('Build'){
  def mavenHome = tool name: "maven3.8.5"
sh "$mavenHome/bin/mvn clean package"
}

-------------------
** Generate Sonarqube report

node{

def mavenHome = tool name: "maven3.8.5"

//checkout stage
stage('CheckoutCode'){
git branch 'development', credential id----------This can be generated using snippet
}
//Build stage
stage('Build'){
sh "$mavenHome/bin/mvn clean package"
}
//sonarqube stage
stage('SonarQubeReport'){
sh "$mavenHome/bin/mvn soanr:sonar"
}

}//Node Closing
----------------


** Upload Artifact into Artifactory repository

node{

def mavenHome = tool name: "maven3.8.5"

//checkout stage
stage('CheckoutCode'){
git branch 'development', credential id----------This can be generated using snippet
}
//Build stage
stage('Build'){
sh "$mavenHome/bin/mvn clean package"
}
//sonarqube stage
stage('SonarQubeReport'){
sh "$mavenHome/bin/mvn soanr:sonar"
}
//Nexus Artifactory
stage('Nexusdeploy'){
sh "$mavenHome/bin/mvn deploy"
}

}//Node Closing

------------------------------

** Deploy Application into Tomcat server

node{

def mavenHome = tool name: "maven3.8.5"

//checkout stage
stage('CheckoutCode'){
git branch 'development', credential id----------This can be generated using snippet
}
//Build stage
stage('Build'){
sh "$mavenHome/bin/mvn clean package"
}
//sonarqube stage
stage('SonarQubeReport'){
sh "$mavenHome/bin/mvn soanr:sonar"
}
//Nexus Artifactory
stage('Nexusdeploy'){
sh "$mavenHome/bin/mvn deploy"
}
//deploy to Tomcat server
sshagent(['This is pipeline snippet code, add credentials and generate and paste, it looks like this']){
  sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@tomcatIP:/opt/apache-tomcat-9.0.60/webapps"
}

}//Node Closing

scp to copy command
-o options to select
stricthostkeychecking=no       because This helps to bypass Prompt "Are sure do you want to connect to server" as we are deploying auto we dont want barriers..



The Package is already created we need to just copy from one server to another server A to Tomcat sever and hence Just copy from and to path and Job is done..
Generate a token using SSH Agent Plugin, Install the plugin to see the snippet code in snippet generator..

Instead of password we can use "PEM file key of TOmcat Server if we dont have Password"

jenkins Credentials

Global Credentials
SSH Username with private key
username:tomcarusername
copy the pem contents and paste it here
description:Tomcat credentials

click on Add

sshagent snippet 
select credentials of tomcat 
generate pipeline script

and paste it 


Add into pipeline 

and build now..

Permisison denied error: Check permission whether webapps directory has write permissions, if not chnage the permissions..

//sigle line comment

/*
Multiline comment
*/
......................................................................................................................................

# can we keep Jenkinsfile custom name??

The Jenkinsfile is Default pipeline Script name, but we can edit the file and give Custom name also...

For Custom Name we need to configure in Jenkins also in Scipth Path Section with Same name

save it, it will work.

The Jenkinsfile should be in github and it will be sourced from git to Jenkins..
.......................................................................................................

Checkout for Global env Variables Refernces in Dashboard.....pipelne scripted way......Pipeline syntax.......Global Variable Refernce

we can use env variables in script and work it across the pipeline

env.BRANCH_NAME
env.NODE_NAME

echo "The Node Name is ${env.NODE_NAME}
echo "The Job Name is ${env.JOB.NAME}
echo "The Build Number is ${env.BUILD_NUMBER}


# PIPELINE SCRIPT

node{

buildName 'Dev - ${BUILD_Number}'
buildDescription 'Pipeline Script - Scriptedway'

def mavenHome = tool name: "maven3.8.5"

echo "The Node Name is: ${env.NODE_NAME} "
echo "The Job Name is: ${env.JOB.NAME} "
echo "The Build Number is: ${env.BUILD_NUMBER} "

//checkout stage
stage('CheckoutCode'){
git branch 'development', credential id----------This can be generated using snippet
}
//Build stage
stage('Build'){
sh "$mavenHome/bin/mvn clean package"
}
//sonarqube stage
stage('SonarQubeReport'){
sh "$mavenHome/bin/mvn soanr:sonar"
}
//Nexus Artifactory
stage('Nexusdeploy'){
sh "$mavenHome/bin/mvn deploy"
}
//deploy to Tomcat server
sshagent(['This is pipeline snippet code, add credentials and generate and paste, it looks like this']){
  sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@tomcatIP:/opt/apache-tomcat-9.0.60/webapps"
}

}//Node Closing


-------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Declarative Way

pipeline{
  //agent any
   
  or 

  agent{
  label 'nodename'
  }

}
----

Declarative pipeline to build and create a package.

pipeline{
 agent any

 tools{
 maven "maven3.8.4"
}
  
  //Get the code from git hub
  stages{
    stage('checkoutcode'){
      steps{
        Copy and Pate the snippet code
      }
    }
    
   //Do the Build
   stage('Build'){
     steps{
       sh "mvn clean package
      }
   }
  }
}

------

Execute Sonar Report

Declarative pipeline to build and create a package and sonar report.

pipeline{
 agent any

 tools{
 maven "maven3.8.4"
}
  
  //Get the code from git hub
  stages{
    stage('checkoutcode'){
      steps{
        Copy and Pate the snippet code
      }
    }
    
    //Do the Build
    stage('Build'){
     steps{
       sh "mvn clean package
      }
    }

    //Generate sonarQube report
    stage('SonarQubeReport'){
      steps{
        sh "mvn sonar:sonar"
      }
    } 
  } 
}

----

Upload Artifacts to Nexus Server

pipeline{
 agent any

 tools{
 maven "maven3.8.4"
}
  
  //Get the code from git hub
  stages{
    stage('checkoutcode'){
      steps{
        Copy and Pate the snippet code
      }
    }
    
    //Do the Build
    stage('Build'){
     steps{
       sh "mvn clean package
      }
    }

    //Generate sonarQube report
    stage('SonarQubeReport'){
      steps{
        sh "mvn sonar:sonar"
      }
    } 
    //Upload Artifacts into Artifactory
    stage('Nexus'){
      steps{
        sh "mvn deploy"
      }
    }
  } 
}

-------
Deploy app into tomcat server

pipeline{
 agent any

 tools{
 maven "maven3.8.4"
}
  
  //Get the code from git hub
  stages{
    stage('checkoutcode'){
      steps{
        Copy and Pate the snippet code
      }
    }
    
    //Do the Build
    stage('Build'){
     steps{
       sh "mvn clean package
      }
    }

    //Generate sonarQube report
    stage('SonarQubeReport'){
      steps{
        sh "mvn sonar:sonar"
      }
    } 
    //Upload Artifacts into Artifactory
    stage('Nexus'){
      steps{
        sh "mvn deploy"
      }
    }
    //Deploy App into Tomcat server
    stage('TomcatDeployment'){
      steps{
        sshagent(['--------sshagenttokenwhichisgenertaedfromsnippet']) {
          sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@tomcatIP:/opt/apache-tomcat-9.0.60/webapps"
        }
      }
    }
  } 
}

# Declarative snippet generator:
agent:

environment:

input:

matrix:

Options: If we want more feature of pipeline like discard old build, Timestamps and all such options we can generate Deleclarative Snippet generator and paste it before the "stages section"

Triggers section: can create poll scm and trigger timeline configurations of git and can generate the snippet and add before stages

parameters:

Post stage or Build Conditions: we can give post conditions also, if it is sucess do this, if it is failed do this, After stages we need to add this section..

libraries:

stage:

stages:

tools:

triggers:

When condition:

-------------
................................................................................................................................................................

# Multibranch Pipeline

Assume for a Repository we have 50 branches, WE NEED TO CONFIGURE IN JENKINS

We use Multibranch Pipeline project

we need to give git Url of that project and 

It uses Scriptfile what ever the file-name we have given in jenkins UI, IT will findout in every branch and it executes it..

If you want to create a Multi branch pipeline the product code should have pipline script or not???

No without Pipeline script we cannot create..

The Multi branch pipeline searches Github by timeline which we give......like 1 minute 30 min options are available in UI
.............................................................................................................................................................

# sys config and Admin


* In RHEL

cd /etc/sysconfig/
pwd
ls -l
nano jenkins

you can do chnages of system configuration related to Jenkins 

like Home directory

JENKINS_HOME=var/lib/jenkins

JENKINS_USER="Jenkins"

JENKINS_PORT="8080" and chanage where ever 8080 is there in that file

we have to restart Jenkins server to affect the changes

systemctl restart jenkins

systemctl status jenkins

systemctl stop jenkins

systemctl start jenkins

or

service jenkins stop

or

system ctl daemon-reload
systemcl restart jenkins


* In Ubuntu

/etc/default/jenkins


# Views

If the Jenkins is having N number of Jobs, we are going to create Views to Differnciate the projects who work on Other projects..

Add + symbol in Dashboard

Give Name

List View

Jobs
Select your Jobs Select the jobs which you want to Display as view

save it


We can create How many Views we would like to create 


Edit View to add new projects to Existing View Config...

Delete View.....To delete the View clck on delete the view
The Only View is going to Delete it No the Job...

Under View All you can see All Jobs..

Views can be used to Group the relevant Jobs...

# Security

Security-----Manage Users---Create USers...

Configure Global Security..

Security and permission to users
The Users details store in jenkins User database.


* Jenkins own database             (Normally manual users data is stored here)

* LDAP: If we Integrate Server we dont need to create Users Manually  (In Real time Users config using this LDAP)

     server Url:
     Advance server config:
     root Dn
     User search Base
     User search filter

* Authorization
     Logged in users can do Anything   (default) behave as Admin

     Matrix based Security
     Project based Matrix Authorization startegy

If we install Plugin Roll basedAuthorization strategy also


we can select Project based Auth strategy we can give permission of access to certain Jenkins tasks and features

we need to click on Add User or group and give permissions to jenkins App

we levels such as 

Overall   Credentials    Agent    Job   Run   View    Job config history   SCM    Lokable resource


In This Sections we need to give tick marks for users who should be given what..


.....

# Backup

Manage Plugins

Click on Available

Thin Backup plugin
Periodic Backup Plugin
Backupp and Interrupt Job Plugin
Google cloud plugin

we can restore job config using Periodic, backup and interuppt

Thin backup: Using this plugin we can take backup of Jenkins Configurations

-Backup Now 

-restore 

-Settings

We need to configure where we need to do backup for Jenkins

Go to setiings tab

what we need to back up

where we need to store

create a directory in Jenkins server with name jenkinsbackup

Jenkins Backup

The folder what we created is going to use by jenkins user so if we want to have access for that we need to change access for all 

chown -R jenkins:jenkins jenkinsbackup

ls -l

user and group name has been changed

Explore the commands and requirement and change the parameters and click on backup now the backup is taken to specific folder

Explore settings section and do the rest..

* Restore Configuration

Go to thin backup plugin----select date of backup which is created -----click on restore.
...................................................................................................................................................................

#  Migration

Aws Linux Server ------100 Jobs---------I want to transfer to some other server Migrate----------------------Azure/GCP server------------------

Assume our server with Jobs is in AWS

Install Jenkins Server with same version in some other sever like Azure/GCP

rename the Home Directory to

The default home directory is /var/lib/jenkins

Rename it to /var/lib/jenkins_bak   (Jenkins_bak means backup, we are creating _bak so that Jenkins cannot recognise the directory)

copy the Home_Dir of AWS jenkins TO Azure Jenkins

and some configuration Files

If you dont have to AWS server we can install a plugin called as, Job Import Plugin, The Pluging has to install in New server

Jenkins Source URL

and Username and password 

and All jobs are transffered...

Refer Job Import plugin usage in Youtube
....................................................................................................................................................................

# Jenkins shared Librarire

Jenkins Shared Libraries is the concept of having common pipeline code in version control system that can be sued by any number of pipelines just by refering it, Infact multiple teams can use it the same library for thier pipelines.

we will be keeping in Source code Management 

we are resuing those source code of scripts in our Jenkins Project..


Step 1 
Directory structure
The directory structure of a Shared Library repository is as follows: 
(root)
+- src # Groovy source files
| +- com
| +- mss
| +- deploy.groovy # for com.mss.deploy class
+- vars
| +- build.groovy # for global 'build' variable
| +- build.txt # help for 'build' variable
+- resources # resource files (external libraries only)
| +- com
| +- mss
| +- help.json # static helper data for org.foo.Bar
src: The src directory should look like standard Java source directory structure. This directory is added to the 
classpath when executing Pipelines.
vars: This directory holds all the global shared library code that can be called from a pipeline. It has all the library 
files with a .groovy extension.
resources: A resources directory allows the libraryResource step to be used from an external library to load 
associated non-Groovy files. Currently this feature is not supported for internal libraries


Step 2:
Add GitHub Shared Library Repository to Jenkins
Go to Manage Jenkins –> Configure System, then 
Find the Global Pipeline Libraries section and add your shared libraries repo details and 
configurations as shown below. 


Step 3: 
To access the shared libraries, in the Jenkinsfile (declarative pipeline) needs to add the 
@Library annotation, specifying the library’s name as follows. 
@Library('msssharedlibs') _
pipeline {
 agent any
 stages{
 
 stage('CheckoutCode')
 { 
 steps
 { 
 git branch: 'development', credentialsId: '6773dc34-a3fd-44ec-b1ee3d2f0aa9f346', url: 'https://github.com/DevOps/maven-webapplication.git'} 
 } 
 } 
 stage("Build"){
 steps{
 stages("Build")
 } 
 } 
 
 stage("Execute SonarQube Report"){
 steps{
 stages("SonarQube Report")
 } 
 } 
 stage("Upload Artifacts Into Nexus"){
 steps{
 stages("Upload Into Nexus")
 } 
 } 
 
 }// Stages Close
} // Pipeline Close
To get the build parameters… 
parameters { 
 string(name: 'GoalName', defaultValue: 'Package', description: 'Pass the Maven Goals') 
 choice(name: 'BranchName', choices: ['master', 'development', 'stage'], description: 
'Pick the Branch Name.') 
  

stages{ 
 
 stage('CheckouCode') 
 { 
 steps 
 { 
 git branch: "${params.BranchName}", credentialsId: '6773dc34-a3fd-44ec-b1ee3d2f0aa9f346', url: 'https://github.com/TechnologiesDevOps/maven-web-application.git' 
 } 
 } 
Note: Here you must use the "" quotes.

..................................................................................................................................................................

# Upsteam job and Downstream job

The Dev job is upstream for qa

The QA Job is DOwnstream job for dev and also Upstreanm job for prod

prod  Downstream for QA

These Upstream and Downstreamjobs helps to trigger the pipeline one another

If Dev is finshed start QA and If QA is finsihed start Prod

Like this we need to configure Upstream and Downstream jobs


Build Trigger:

Build After other projects are built

This option helps to trigger the Up and down stream Jobs


Trigger only if build is stable
Trigger even if build is Unstable
Trigger if Build Fails
Always trigger even if build is aborted

These Jobs Trigger each One another if conditions are met.....

In scripted way using snippets we can configure it

# Slack Integration

We can use app or in web browser if we dont have app 

For email triggering of Notifications we use SMTP server and do configurations

* Create channel in slack

* Build-channel (Private)

Add people in channel who are working in team

Right click-------setting and Admin-----Manage App------Slack app directory

Search------jenkins-------click on this jenkins CI-------------Add to slack

Choose the channel to Post

----Slack Notification Plugin should be installed In jenkins

Do settings

configure system

and Follow process in Slack app directory for Next Steps and More settings and configurations..

Slack Notification in postbuild section in Jenkins

Notify Build start
Notify succeess
Notify Abroted
Notify No Build
Notify Unsatble
Notify regression
Notify Failure
Notiy Back to Normal
Notify Every failure
Notify First Failure
Notify repeated Failure Only
Include failed Test
Include Custom Messages 

What commit Information to Include
common list with Authors only

save by selecting any one of preferences

we can generate code snippet in pipeline script and configure it..

.................................................................................................................................................................
# Build with Parameters

Building with Parameters is noting but building a project with choices and conditions

like Master, branch, Dev, Test, QA.


# Master and Slave Concept..


Master Instance is a primary sever which is configured and 

The Slave server needs to Install Java only not Jenkins

The slave machines can be created in any Operating system..

If we trigger all jobs at a time it will take more time, if we distribute jobs, it will complete the build..

To improve the Performance we are using Master and Slave Architecture



we can call as slave or Node


Master................Slave1.....Slave2......Slave3.......

we will configure jobs based on server configurations.

1 Node we are using One kind of Apps

1 Node we are using Kind client Jobs

So on...

We are going to create slaves but it is necessary to install java..

The Jobs Information is Stored in Master Instance...Not in slaves

The Slaves are used to give computation power and triggered the JOB 
The code which is cloned from github is stored in Slave instance so that it can work and info is available in slave..

In slave servers we dont install Jenkins..

The Slaves can be created in Any Os 

Can we give same name as slaves for all these slave instances, we can label as same name for all instances.??
If we give same name all three instances, where ever slave is available the job is going to run.

If we give a slave a name manually slave1 slave2 
This will create a specific work to slave names
The particular Jobs are going to work on these slaves, This might not create auto assign a jobs and some resources be free.

The advantage of giving same label to slaves is, it will execute jobs depends up on availability, if a slave is free, it gets assigned.

Go to settings and COnfigure nodes as Default is "Built in Node" Add node using SSH Connection and configure it..

pipeline{
  agent{
    label "slave"
  }

  parameters {
    choice choices: ['master', 'uat', 'qa', 'test'], description: 'select the branch name', name: 'Branch:Master...
  }
}

we can configure no of executors That is Jobs which can run at a Time..On Each slave we can configure it..

..................................................................................................................................









