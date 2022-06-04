# Maven

Application Servers such as JBoss/Wildly/WAS/Weblogic/Tomcat

We need to create a package in order to work the source code

Maven is one of the popular build tools

What this Build tools are going to do?

This build tools are going to create Packages

Each programming languages we have build tools

In Java we have ant is there, Maven is there, gradle is there...

In .Net we have other tools such as Nant/MS Build

Python -----PyBuilder

Ruby------Rake

As a developer along with the source code, He is going to write a Build Script

He is going to create a package for source code

so we have decided 

Maven is Build tools for Java Projects, Ant is legacy one, Gradle is latest and many people one are not adopted
Maven has many features than all hence we are using maven

Most of the applications are developing using JAVA as it is opensource

for Dot net we need to purchase License from Microsoft

Maven is open source as free to use and used only with JAVA, They used JAVA to develop the Maven applications.

I want to create a package for java source code using any one of the JAVA build tools we create packages that process is called as Build.



We have various JAVA Packages 

Oracle JAVA
OPEN JDK
IBM JDK

Who developed Java, It is Sun Microsystems, The sun microsystems is acquired by Oracle

we Can Build Various Applications such as 

Standalone Applications
Web Aplications 
Enterprise Applications 

If it is a standalone Application it contains JAVA code

If it is a web Application it contains (HTML/css/javascipt/xml/images)

In Enterprise Applications we have Multiple Modules.

I have Hello.Java code "this is one Java code"
How can we run this java code

For this we need to we have to complie the java class

javac helloworld.java 

javac is command to compile 

once if u compile it will create a file called JAVA.class

Hello.java..............Source code
Hello.class..................Byte code

So the source code can be able to understand by Human and Byte code is not understandable by human
Only Byte code is understand by Java Virtual Machine..

so How can we run this Java class
java Hello world      ............... This runs Java class

So like this we can run the Java Programme

Standalone conatains a JAVA code as we know we create a package called as (JAR ---JAVA ARCHIVE)
WEB Applications we create .............(WAR ----------WEB ARCHIVE)
ENTERPRISE APPLICATIONS -------------(EAR -----Enterprise ARchive)

The Jar File contains basically .classfiles + Manifiest files, It doesnot contain any web contains

The WAR file contains some JAR files and Web contains

EAR file contains, It contains Ennumber of Standalone and web modules as well as resource files.


The WAR file doesnt have manifest file "NO"  In this manifest file we specify what is the starting point of application which Java class need to use.

If we want to run this EAR package atleast u should have one WAR file, If we have three webmodules it contains 3 WAR files

if it is 10 Standalone Applications modules it contains 10 JAR files...

As a developer they will take care of all these things

As a DevOps Engineer we should know how to build the Packages...

The EAR Packages are bigger packages, Based on Project we are going to create and choose packages.

# Maven Directory Structure

Maven is not Executable software like exe packages like in windows

We have to download Archive flle set path and we have to use it..

It is called as Apache Maven or Maven, All the softwares almost are Opensource from apache..

If we want to use Apache Maven 
use 
Go to Apache Downloads website

Binary is when we need to use features and there is no customization of features....

Source is When we want source code also, if we want we can enhance the existing features on top of that...

apache-maven-3.8.4-bin.zip

If we want to install in server use wget command

wget download url 

After extracting the ZIP, it contains \\ Totally 4 Directories....

bin: Binary files
conf: configuration files
       In this we have settings.xml 
lib: libraries
           If a software which is devolped in java we see all jar files, basically it contains Java libraries...
boot: it contains files which are used at run time

# Maven Installation
To Install Maven we need to first install JAVA as it is devloped by using JAVA
 Maven 3.8.4 is latest version
to install maven which version of java is used as version compactability is important
JAVA 1.5 or JAVA 5 both are same

Always check system requirements in offical page of maven to check compactability of verison...

Maven 3.3+ is required JDK 1.7 or above to execute

JAVA 1.7 is also called as JAVA 7 

can we used JAVA 1.8 ....YES we can JAVA 8 

JDK  ........Java Development Kit

JRE .........JAva Runtime Environment

Both are different, basically to support an application dependency we use JRE and if we want to develop the JAVA softwarare we use JDK.

Javac is not going to work if you install JRE

How to know if you have installed JRE or JDK???
javac --version if we get output means JDK is installed
if it says 
javac --version  command not found, It means JDK is not installed

TO INSTALL MAVEN we need to install JDK Only....

IF WE INSTALL JRE The Maven is not going to work...

How to Install Maven in Java Lnux server...

# How to Install JAVA-11 in Ubuntu
sudo apt update
sudo apt install default-jdk
java -version
Output:
openjdk version "11.0.2" 2019-01-15
OpenJDK Runtime Environment (build 11.0.2+9-Ubuntu-3ubuntu118.04.3)
OpenJDK 64-Bit Server VM (build 11.0.2+9-Ubuntu-3ubuntu118.04.3, mixed mode, sharing)

# How to Install JAVA-8.0 in Ubuntu
sudo apt update
sudo apt install openjdk-8-jdk
sudo apt install software-properties-common
sudo add-apt-repository ppa:linuxuprising/java
sudo apt update
sudo apt install oracle-java11-installer
java -version
Output:
java version "11.0.2" 2019-01-15 LTS
Java(TM) SE Runtime Environment 18.9 (build 11.0.2+9-LTS)
Java HotSpot(TM) 64-Bit Server VM 18.9 (build 11.0.2+9-LTS, mixed mode)


To Set Alternative Verisons of Java as Default 

sudo update-alternatives --config java

Output:
There are 3 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                            Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      auto mode
  1            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      manual mode
  2            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      manual mode

Press <enter> to keep the current choice[*], or type selection number:

To change the default Java version just enter the version number (the number in the Selection column) and press Enter.

# Set the JAVA_HOME Environment Variable
Some applications written in Java are using the JAVA_HOME environment variable to determine the Java installation location.
To set the JAVA_HOME environment variable, first, you need to find out the Java installation paths using the update-alternatives command

sudo update-alternatives --config java

OpenJDK 11 is located at /usr/lib/jvm/java-11-openjdk-amd64/bin/java
OpenJDK 8 is located at /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java

sudo nano /etc/environment
JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"
source /etc/environment

To verify that the JAVA_HOME environment variable is correctly set, run the following echo command :
echo $JAVA_HOME
/usr/lib/jvm/java-11-openjdk-amd64

# Uninstall Java
If for any reason you want to uninstall the Java package, you can uninstall it like any other package installed with apt

sudo apt remove openjdk-8-jdk

# TO Check Maven is Installed or not 
mvn -verison

# Refer Mithun technologiess Blog to Refer Install and Uninsatll in Redhat Linux servers

https://mithuntechnologies-devops.blogspot.com/

http://mithuntechnologies.com/devops/DevOpsToolsMithunTechnologies.html

Download links will expire and version changes as time goes on...., go to offical page and copy links and modify and paste in Linux servers...
Follow the Instruction to avoid Errors

yum install unzip -y
unzip zip_file_name

tar -zxvf apache-maven-3.8.4-bin.tar.gz

After extracting_go to that insatlled directory\\

The Installed directory is called as home_directory

we need to assign Env Variable to assign the MAVEN home directory as system and Dependencies can understand that MAVEN is Present here.

Follow more the blog ...

mvn -version

To Install JAVA in Windows JAVA_HOME   M2_HOME are ENV variables for windows 

we get errors if we dont install it properly...

Refer Mithun Technologies Videos of Youtube channel to learn more...

# What are the Contents in POM.XML 

The build tool has default script file,

ANT ---> build.xml

MAVEN ----> pom.xml

Gradle ----> build.gradle

Can we give custom names like

facebook.xml ....Yes it is possible to give

Each build script we have default file name for Maven it is pom.xml

In POM.xml we have Project tag that is called as 

Parent Tag/Root Tag
<project>

In HTML all the tags are predefined and Clsoing tags are not that Mandatory ...

In XML we have Predefined as well as custom defined Tags
Like
Each open tag should have a closing tag...


<project>
has a opening tag as well as closing tag

it has sub tags also like

<groupId> we have company name like com.facebook or we give project_name also </groupId>
<artifactId>facebook we can give company name </artifactId>
<version>1.0.0 we can give version </version>
<packaging>using maven we create many java packages like jar,war,ear what ever u specify it will create</packaging>

<dependencies>
     Inside depenencies tag we can specify n-number of dependencies, to run an facebookapp we can run dependencies
  <dependency>
    <groupId>junit</groupid>     
    <artifactID>junit</artifactId>
    <version>3.8.1</version>
    <scope>test</scope>
  </dependency>

</dependencies>

</project>

#The Junit is used to run the Unit test cases,Devlopers write test cases so that programm can run 
#The Test cases will look like HelloworldTest.java---->Test cases file which has key word test 
#To run this unit test case we are going to use this JUnit Dependency, so like this as a developer, he is #going to add ennumber of dependencies, as a developer he knows what dependencies are required to build a #package, As a devops engineer we should know what are these tags...What purpose it is going to use..

He wont write all dependencies from scratch, he is going to write from one of the repository which is laready exist
maven central repository
https://search.maven.org, we can search in this repository of dependency name and click verison which to use and it will be giving code snippet and copy and paste the dependencies....All these dependencies will be taken care of developer..

For every dependency we have a scope as above, The scope represents this dependency is used when u are running test cases, some dependencies run when it is compiled or running the programm, The developer will specify it...

we add Dependency as per our part of project in POM.xml, so if we want to run the build script we are going to run commands such as
mvn package, so when we execute mvn package, it is going to create a package the name we specified,
Before creating a package it will first get and download dependencies in the system what ever we have assigned in pom.xml, it will get it from 

Maven repository, it has Three repositories

Maven Local
Maven Central
Maven Remote

The local repository the files which are downloaded are stored in .m2 folder ~/.m2/repository
so it is going going to search in .m2 folder

In windows in C drive in users directory and in users name, you will find c:\\Users\syed\.m2 

In MAc /users/syed/.m2/repository

This default path for Linux and Windows and mac for repository.

First the Maven searches for local repository if the plugins are available or else it will go to Maven Central repository.

# Is it possible to change default path to Custom path for maven

settings.xml  which is available in conf directory

open that settings.xml file 

<localRepository> Here keep the path </localRepository>    In this file..
Update the path where u want to create the local repository.

Maven Community team take care of Maven central repository, The Maven Central repository is used when maven doesnot find libraries in the local repository..

Maven should have internet connectin when it performs to download libraries from Maven central repository

# Remote repository

Remote repository is managed by each organisation and Maintained by themselves for thier project need and usage..

Example: Flipkart has developed 10 Jar files,how we should share these 10 jar files, through communicator or email??
Not at all
Through remote repository of organisation not git also...we will create repository through that we are going to share

we will create repository by tools such as Nexus, Jfrog, Artifactory using that we use the repositories...

Why cant we share these jar files with Maven repository??? and community team to upload it??
Because we are making Public and public will download depndencies 
we have created for organisation purpose, hence we are going to upload, we are configuring the repository Url in Pom.xml and it will download the dependencies and it is accessible with in organization only..


Local Repository <...............> POM.xml <..................>Central Repository
                                   Maven   <..................>Remote Repository
                                    .
                                    .
                                    .
                                  .Site.

If we want we can specify condition to download only from that repo itself also..

Each Developer has his own local repository, if u download a java project and build using maven a repo is created automatically..
Even in lappy also it will be going to create, 
Cental repo can access by anyone, it will be One repository...
Each company can have ennumber of repositories...

# Maven Lifecycles:

Three Lifecycles in Maven has Maven and each lifecycle has coressponding goals..

Lifecycle                                 Goals
Clean                                     Clean: It will deletes the previous build files.
site                                      site: It will generates the documentation for the source code.
                                                Without writing the documentation manually u can genearte it, but it is old method
                                                Now a days Dev teams are using swagger tool to Automatically generate documentation for code.
default                                   default: It contains many goals which are default, but we are not using it as default,Like
                                                Validate:it will validate dir structure and files
                                                complie: it compiles the source code and Junit test cases code
                                                test: It will run the Junit test cases,whcih dev has written while developing.
                                                       Java---> Junit
                                                       .Net---> Nunit
                                                        C-----> CUnit
                                                        C++---> CPPunit
                                                        Nodejs--> jasmine.
                                                      These test cases are written by developer,if you run this goal test cases runs
                                                Package:It will create the Package based on the Project type like (jar,war,ear)
                                                        which we have specified in packaging tag in pom.xml
                                                install: It will store the build artifact/package in Maven Local Repository
                                                Deploy: It will store the build artifact into remote repository

What is the command to Run the Unit test cases:
mvn test
If we want create a package:
mvn package
if we want to delete the previosu build files
mvn clean

can we use like "mvn clean package" can we use along with one or more goals??? YES we can use
Which goal is Execute first??
It will Execute from Left to Right Order, First it will clean and package it as per above example...

Can we use like this one "mvn package clean" No use at all as it creates package and deletes it...

" if we give mvn deploy can it pass all the goals"   NO

When we give command we need to pass Lifecycle and Goal............

if we want to execute mvn test, what goals it will execute first 
it will execute validate,compile and test 
The goals will run in order 

if we give mvn deploy, it will execute from top to bottom
validate
compile
test
package
install
deploy

if any one of the goal is failed, in test goal it will not continute and stopped and not executed...Even if one Unit test case also fails it is going to stop the process..

It will be executed again from first and executes till end after fixing one issue also, it wont run only one test case next time....

Is Unit test cases are Important >>> YES it is ....As DevOps Emerged we are writting Unit test cases to automate

# Is it possible to skip Unit Test cases>>>>>>YES it is Possible to do

Just execute mvn clean package -DskipTests

it is going to skip the Test cases 

or

mvn clean package -Dmaven.skip.test=true

It is going to skip all the test case, using these two options

we cannot skip other goals as example without compile we cannot create packages
..............................................................................................................................................

We get Error when we execute mvn commands in linux machine, Like The goal you specifies requires a project to execute but there is no POM in directory(/root). Please verify invoked Maven from coreect directory

...> Go to JAVA Project Application directory which you have cloned from git

....> You will find POM.xml file and SRC directory

In SRC Directory we Have, Note: Do tree command in directory to vizualise the directory

SRC......> (MAIN       AND        TEST)  Directories

Main Directory conatins source code

Test Directory contains the test cases

Mian Directory.....>java....>com....>mt.....sample......HelloWorld.java

Test Directory......java....com.....mt....sample....test....HelloWorldTest.java

This is Standalone Application hence we give "jar" in POM.xml in packaging section.

Go to Pom.xml location path and execute command "mvn package" 

This will Install and download libraries from central to lcoal, if u are running it for first time and execute the goals and build the package, if any erorr it will terminate

The Snapshot what you see in screen is called as Jar package where this file can be deployed in Web server

Follow Blog for Installation and COnfigurations if you get any errors related to maven or java

For code errors Devloper such be responsible to fix it

When u compile the application using mvn compile it will create java.class file in taget folder

When u package the application using mvn package it will create javaapplication_snapshot.jar

The Package is created in folder of JAVA application with name /root/javastanaloneapplication/target/maven-stanalone-application-0.0.1-SNAPSHOT.jar 

Depends up on command what u give it does the job...

If u Do another Project in same server you will find it same location and places and the exisiting libraries also wont be downloaded again and again by maven if it is already existed in local repository..

Always check console how goals are getting executed and for errors also...

mvn clean will download related plugins and it will clean the target directory.......

It will not perform any task, just it will clean it..

mvn clean package:

It will clean\
validate\
compile\
test\
package\

In sequence it runs and stops the maven goals

cd ~/ .m2/repositories "All the dependencies and libraries are stored in this path"

# changing local repo to other location..

create a folder and pwd the location and copy path 

settings.xml is present in cd/opt/apache-maven-3.8.4/conf/

nano settings.xml

scroll down

go to section called as

Line number 49 commented as <!---- opening the comment

In between if you keep any thing it will ignore

----> Closing the comment in xml

The default path is commented, check it if not comment it and 

copy and paste in line numebr 55 as or any line below it

This will work as custom repo

<localRepository>/root/mvnlocalrepowhichyoucreatedmanuallypathpastehere/</localRepository>

When you change the local repository path to other folder in settings.xml file, it will not recognise previous path hence it will download 
libraries to new path and configure dependencies again...

If the Maven folder and libraries are in two places what will happen???
it will give preference to settings.xml path what u have given..

"mvn clean package -DskipTests"   will Compile and skip Unit Test cases
"mvn clean package -Dmaven.test.skip=true" will skip compile and unit test cases also 

# mvn install

In maven Local repository we have many directories

such as libraries and dependencies folders 

in that we have directory.....> COM

The Install commands is going to store the artifact depends up on the group name

What is the group com.mt is the group name

cd com.....>google.....> as by default

after using mvn insatll

It is going to create Artifact id with the name and it is going to install here..

/root/maven-standalone-application/pom.xml  TO /root/mvnlocalrepo/com/mt/maven-stanalone-application/0.0.1-SNAPSHOT/maven-standalone-application-0.0.1-SNAPSHOT.pom

The above path is example of output where it stores the file using install command

The sequence of Steps executes and "package-snapshot.jar" also would have been stored in java-application-proejct-directory also 

# mvn deploy

It is going to store in remote repository if you config it.....It is not going to work 
When we install Nexus in system we can execute it..

# Web Application Architecture of JAVA

src Folder Contains

src..............>(main     and  Webapp) Directories

here in web application we dont have Test directories as we seen in standalone application

Main.....>java......>com.......>mt......>service......>Employeeservice.java

webapp......>images.....>jsp.....web-inf

we would been having 

test directory also

If you dont see any test cases directory, there is no test cases written for that project 

IT will be creating WAR file using pom.xml configurations and name...

<groupId>com.mt</groupId>
      <artifcatId>maven-webapplication</artifactId>

using groupid_artifactid_packaging version_packaging-Type

Example: maven-web-application-0.0.1-snapshot.war

It is availble in target name...

Why it has created custom name for war file?????
we are using tag such as 
<finalName>maven-web-application</finalName>

What ever the name we specify here it will be created cutomized way for war file or else it will create as per above..

# Enterprise Application

Each Module has a pom.xml for EAR based application

For whole project also we have a pom.xml 

MAven-Enterprise-app (FOlder)

Maven_enterprise_app-ear.......>pom.xml(child_pom_file)......>src....>main......>application....META-INF......>MANIFEST>MF

Maven_EnterpriseApp-web........>pom.xml(child_pom_file).......src.....main....java....com....mt...HelloWorlcontroller.java
                                                            main.....>webapp....>web_inf
test............>java...........>com.............>mt.........>TestController.java

pom.xml(parent pom.xml)   which is present in folder of project.


If multiple modules are there for every module is there a pom.xml????

Each Module wheather it is standalone module or web module each module it contains pom.xml

Suppose if 4 web modules are there 4 war files are going to create....and it is going to add in EAR file

so we have one web and one ear module with pom.xml  .......>only one ear is been created

<modules>
  <modules>MavenEnterpriseApp-ear</module>
  <module>MavenEnterpriseApp-web</module>
</modules>

if you see this Modules_tag this means it is Parent pom.xml file
here we are going to add n number of modules in this modules tag

For child pom.xml it contains <parent> </parent> tag details so that it can match with parent pom.xml file

After Using mvn package it has created a ear file and lcoated in target directory of the project_application_location

Where you have created and cloned from git.......if u have moved it presents there.....

# So all These commands can work in Normal User also for that you need to install maven in global level

If you want to configure maven in global level, you need to configure settings in the /etc/profile

There you can configure it globally...


# Assume Enterprise Application has n number of modules as i want to work for specific module in that is it possibe

Yes it is possible

How to do it

so, first we need to check how many modules are there in pom.xml in parent pom.xml in modules section or Go to project_application_dir

pwd project parent directory 

Assume we have three modules in that directory

copy the module dir_name which you want to build it asume it is "MavenEnterpriseApp-web"

and type this command being in that project_app_path directory where you see modules

"mvn clean package -pl MavenEnterpriseApp-web"

"-pl means project list"  ,comma seperated you can specify n number of modules in single command

Without .war we cannot execute .ear 

POM= Project Object Model.

what are build env, for each env we have properties file.....

dev
dev.properties


qa
qa.properties


prod
prod.properties

so when we do mvn clean package based on my env it has to take 

suppose if i want to do dev, specify

mvn clean package -Pdev
-P means Profile

earlier we use to use profile concepts now a days we dont use it..........

.....................................................................................................................................


Other Topics:
Packages:

Java ....... jar/war/ear
.Net ....... .exe
Node.Js .........No packages
Python ..........No packages

pom.xml we have many dependencies
package.json ........have many node modules





















                                          
                                                    


                                      

                                    





























                                
      















