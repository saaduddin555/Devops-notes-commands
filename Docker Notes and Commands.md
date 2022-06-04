Docker Is a containerization software using which we can create build and deploy our applications as containers.

The Docker uses Host Os and Kernel and \\

The container will have softwares and libraries and applications

Containers is light weight and Container doesnt have Os and containers uses Host Os and kernal as well as system resource

In Linux we have concept of 

Namespaces and Cgroups
User space
process space
storagespace
 
Container will not have full blown Os, It uses host Os and kernal resources and physical resources


Docker is for Devlepors, Admins(DevOps) to build,ship and run applications as contianers.
.......................................................................................................................................................................
Docker Editions:

Docker CE --> Comunity Edition --> Open Source(Free)

Docker EE --> Enterprise Edition --> Commercial

Type: Containerization
Vendor: Docker INC

O.S --> Cross Platform(Docker can be installed in any O.S)

Docker Can Be Installed in Linux, Windows OS ,mac OS  

Docker CE Can be installed in Most of the linux except redhat.

Docker EE can installed in all O.S including redhat.

Docker CE --> OpenSouce Free

Docker EE --> Commerical
   DTR --> Docker Trusted Registry(Private Repo to main docker images)
   UCP --> Universal Controll Pane --> It's GUI for managing Docker Machines

Docker,CoreOS,Rocket,CRI-O,Podman --> Containerzation Platforms/Softwares.
........................................................................................................................................................................

                          Container1                Container2             Container 3

                        Docker Client----------------Docker-----------------Docker Daemon

                                                      os.

                                                 Virtual Machine

Dockerfile --> Dockerfile is file which contains instructions to create an image. Which contains 
               Docker Domain Specific Key Words to build image.
			
		   
* DockerImage --> It's a package which contains everything(Softwares+ENV+Application Code) to run your application.

* DockerContainer --> Run time instance of an image.If you run docker image container will be created
                    that's where our application(process) is running.

* DockerRegistriy/Repository

* DockerRepo/Registry. --> We can store and share the docker images.

* Public Repo --> Docker hub is a public reposotiry. Which contains all the open source softwares as 
a docker images. We can think of docker hub as play store for docker images.

* Private Repo(Nexus,JFrog,D.T.R(Docker Trusted Registory)),
  AWS Elastic Container Registry(ECR)  --> We can store and share the docker images with in our company
  network using private repo

* Docker Enigine/Daemon/Host --> It's a software or program using which we can create images & contianers.

 Docker is cross platform.

Docker CE
   Docker CE will not be supported by Redhat.
   
 
Docker EE
  Docker EE will be support most of the os including redhat.

      
First Create Account in docker hub
https://hub.docker.com

What is docker hub?
It's a public repository for docker images. You can think as play store for
docker images.

# Docker key Terminologies

Docker file is a text file that contains all commands to build an image

Docker image is a file that is used to execute a code in a container

Docker compose is a YAML file that is used to configure your applications services. You can definr and run multiple container applications..

Docker volumes are used for storing and using data by containers, There are 2 type of volumes. Bind mount and tmpfs mount

Docker swarm is a container orchestration tool that manages a group of clustered machines running docker containers.

........................................................................................................................................................................
Install Docker on AWS Ubuntu
############################
sudo apt update -y
sudo apt install docker.io -y
sudo service docker start

sudo docker info

# Check docker is installed or not
   docker info

# You will get permison denied error as regular user dosn't have permisions to execute docker commands.Add user to docker group.

sudo usermod -aG docker $USER 
     or 
sudo usermod -aG docker ubuntu

# Exit From Current SSH Terminal & SSH(Login) again .Then execute 
docker ps


# Amazon Linux
================
sudo yum update -y		
sudo yum install docker -y
sudo service docker start

Add Regural user to dockergroup
sudo usermod -aG docker  <username>

ex:
sudo usermod -aG docker ec2-user

Once you add user to group exit from the server and login again.
# Get docker information
docker info

#Install Docker in Linux (Works for most of linux flavors).
sudo curl -fsSL get.docker.com | /bin/bash


Docker Home/Working Dir: 
/var/lib/docker


Install Docker on AWS RHEL  (Offcially No Support)
############################
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo dnf install docker-ce-3:18.09.1-3.el7 -y
sudo systemctl enable docker
sudo systemctl start docker


sudo docker info

# Check docker is installed or not
docker info

# You will get permison denied error as regular user dosn't have permisions to execute docker commands.Add user to docker group.

sudo usermod -aG docker $USER 
or 
sudo usermod -aG docker ec2-user

# Exit From Current SSH Terminal & SSH(Login) again .Then execute 
docker ps

How many containers we can run in on system/server?
It dependes on your system resources(CPU,RAM).


# List Images

docker images


# Sample DockerFile Content

FROM tomcat:8-jdk8-corretto
COPY target/maven-web-application*.war /usr/local/tomcat/webapps/maven-web-application.war


# Build Image
Defautl Docker file Name: Dockefile
docker build -t <imageName> .

If you have docker file with custom name using -f <fileName> while building docker image.
docker build -f DockerfileMaven -t <imageName> .

Note: Image name should have repository details along with name and version.

Public Repo (Docker Hub)

docker build -t <registryName>/<RepoName>:<version> .

Note: If we don't mention version information. By defualt it will use 'latest' as version

ex:
docker build -t dockerhandson/maven-web-application:1 .


Note: If we don't mention version information. By defualt it will use 'latest' as version


Private Repo (Nexus/JFrog/DTR/ECR)


docker build -t <imageName> .

docker build -t <IP/HostNameOfRepo>:<RepoPort>/<repoName>:<version> .



# ECR --> Elastic Container Registirty

In Case ECR:
-----------
docker build -t 485430697192.dkr.ecr.ap-south-1.amazonaws.com/maven-web-application:1  .


In Case OF Nexus/Jfrog
---------------------

ex:
docker build -t 178.90.34.12:8083/maven-web-application:1 .

Authenticate with repo

# Public Repo Docker hub
docker login -u <userName> -p <password>
ex:
docker login -u dockerhandson -p password


Priavate Repo
docker login -u <username> -p <password>  <URL>



In Case ECR
-----------

docker login -u <username> -p <password>  485430697192.dkr.ecr.ap-south-1.amazonaws.com


Nexu/Jfrog

ex:

docker login -u admin -p admin123 178.90.34.12:8083


docker login -u admin -p admin123 nexus.tcs.com


Push Docker Image to Repo
docker push <imageName>

Public Repo
docker push dockerhandson/maven-web-application:1

Private Repo like Nexus
docker push 178.90.34.12:8083/maven-web-application


Private Repo like ECR
docker push 485430697192.dkr.ecr.ap-south-1.amazonaws.com/maven-web-application:1


Image Commands
=============

# List Images

docker images

docker image ls

# Will return only ids.
docker images -q


# Sample DockerFile Content

FROM tomcat:8-jdk8-corretto
COPY target/maven-web-application*.war /usr/local/tomcat/webapps/maven-web-application.war


# Build Image

Default Docker file Name: Dockerfile
docker build -t <imageTag> .

If you have docker file with custom name using -f <fileName> while building docker image.
docker build -f DockerfileMaven -t <imageTag> .

Note: Image name should have repository details along with name and version.

Public Repo (Docker Hub)

docker build -t <registryName>/<RepoName>:<version> .

Note: If we don't mention version information. By defualt it will use 'latest' as version

ex:
docker build -t dockerhandson/maven-web-application:1 .

Private Repo (Nexus/JFrog/DTR)

docker build -t <imageTag> .

docker build -t <IP/HostNameOfRepo>:<RepoPort>/<RepoName>:<version> .

ex:
docker build -t 178.90.34.12:8083/maven-web-application:1 .

-t -----> Tag-----> <RegistryUrl/RepoName:tag>

# Build Context
What is docker Build Context?

Docker Client will send all the files to the docker daemon which are paert of build context.
What ever files/packages which you are trying to copy to the should be part of your build context means the packages and files should be at one place in that directory.
Docker will build image from build context.

docker build -f <filename> -t <ImageTag> <dockerbuildcontext>

docker build -f javafolder/Dockerfile -t <imageTag> javafolder

instead of Doing as above

Better go inside of folder where Dockerfile is

When "Dockerfile" is deafult name
docker build -t <imageTag> .

Here dot represent (Build context) where . represent to present directory 

When "Dockerfile" is Custom name

docker build -f Syeddockerfile -t <imageTag> .



# Authenticate with repo

# Public Repo
docker login -u <userName> -p <password>
ex:
docker login -u dockerhandson -p password


# Private Repo
docker login -u <username> -p <password>  <URL>
ex:
docker login -u admin -p admin123 178.90.34.12:8083

ECR:

docker login -u <username> -p <password>  485430697192.dkr.ecr.ap-south-1.amazonaws.com

Nexus:
docker login -u admin -p admin123 <Ipaddress:portno>
docker push <ImageTag>

Push Docker Image to Repo
docker push <imageName>

Public Repo
docker push dockerhandson/maven-web-application:1

Private Repo
docker push 178.90.34.12:8083/maven-web-application:1

# Downlod Image from repo
docker pull <imageName>

Public Repo
docker pull dockerhandson/maven-web-application:1

Private Repo
docker pull 178.90.34.12:8083/maven-web-application:1


docker pull 485430697192.dkr.ecr.ap-south-1.amazonaws.com/maven-web-application:1


Inspect Docker Image
==================
docker image inspect <imageId/Name>

docker inspect <imageId/Name>

How to list only layers of an image?
docker history <imageId/Name>



# Delete Image

Delete Image

docker rmi <imageId/Name>

docker rmi -f <imageId/Name>


Note: We cann't remove images if there are running container for the image.We cann't force delete images if there is running container.

If container is in stopped(exited) state we can force delete image for the stopped container.

what is dangling images in docker?
The image which doesn't have repository mapping or tag.

How to delete all the images?
docker rmi -f imageId imageId imageId

docker rmi -f $(docker images -q)

docker system prune 
Will delete all stopped containers , unused docker networks and dangling images.

docker image prune

Will delete angling images.

We can tag image with repo.

# We can use docker tag to tag images with multiple repo.
docker tag <ImageId/ExistingImageName> <ImageName>


# What is working directory of docker?
/var/lib/docker


How can we move/copy images from one server to another server with out repo?

In Source Server(where you have image)
# It save image(All the layers) as a tar file

docker save -o <fileName>.tar <imageName/Id>


Then SCP tar file from Source Server to Destination Server

# In destination server
docker load -i <fileName>.tar


List Dangling images

docker images -f dangling=true

Remove Dangling Images
docker rmi $(docker images -f dangling=true -q)

# docker system prune

docker system prune 

This will remove:
  - all stopped containers
  - all networks not used by at least one container
  - all dangling images

docker image prune
This will remove:
- all dangling images

docker contianer prune
This will remove:
  - all stopped containers

docker network prune
This will remove:
  - all networks not used by at least one container


# How can we move/copy images from one server to another server with out repo?

In Source Server(where you have image)

It save image(All the layers) as a tar file

docker save -o <fileName>.tar <imageName/Id>

Then SCP tar file from Source Server to Destination Server


# In destination server
docker load -i <fileName>.tar


# List Dangling images

Dangling Image is an Image without any repository reference or tag

docker images -f dangling=true

Remove Dangling Images
docker rmi $(docker images -f dangling=true -q)

# How to Tag an image

docker tag <ImageId/ExistingTag> <NewTag>

# docker system prune 

This will remove:
  - all stopped containers
  - all networks not used by at least one container
  - all dangling images

docker image prune
This will remove:
- all dangling images

docker contianer prune
This will remove:
  - all stopped containers

docker network prune
This will remove:
  - all networks not used by at least one container

# What is difference between Docker create and Docker run

Docker create will Just create a container

docker create --name <container> -p <hostPort:containerPort> <Image>
docker run -d --name <container> -p <hostPort:containerPort> <Image>

docker run will create and start running the container.

# can we Mention -p Port forwarding to Existing container

If we dont specify Port number -p or port mapping or port forwarding, It wont MAP with Any Random Host Port

We cannot specify or mention Port forwarding after creation of container..
  
Internally we can access but not outside of docker if we dont specify port Number

remove the container 

create and start using -p option

# How to rename a conatiner

docker remane <containerid/oldname> <newName>


Container Commands:
===================
How to create a contianer?

docker run or docker create

docker create --name <containerName> -p <hostPort>:<containerPort> <imageName>


docker run --name <containerName> -p <hostPort>:<containerPort> <imageName>

# Create a container in dettached mode
docker run -d --name <containerName> -p <hostPort>:<containerPort> <imageName>

what is the difference b/w docker run and docker create?

docker create will only create a container but it will not start the container.
docker run will create a container and start the container.

what is port publish or port mapping in docker ?
If We have to access application which is running as container from out side of docker we can't access using continerIP & ContainerPort. We can publish contianer port using host port using -p or --publish.
So that we can access using HostIP(docker server IP) and Host Port from outside docker.


docker run -d -p 8080:8080 --name mavenwebapp  dockerhandson/maven-web-application

Access Application which is running Using  Docker Server IP & Host Port.

http://<DOCKERSERVERPUBLICIP>:<HOSTPORT>/maven-web-application


# How to create & start container in interactive mode?

docker run -it --name <nameofthecontainer>  <image> /bin/bash

# If container doesn't have bash try with shell(sh)  
               
docker run -it --name <nameofthecontainer>  <image> /bin/sh

# Type exit to come out of the container shell.

List Running Containers
=======================

docker ps 
docker container ls

List All Containers
==================

docker ps -a

docker container ls -a

List only running container ids
==============================

docker ps -q

docker container ls -q


List all container ids
==============================

docker ps -aq

docker container ls -aq


# Start the container
===================
docker start <containerId/Name>


Restart Container

docker restart <containerId/Name>

Stop Container

docker stop <containerId/Name>


# Kill container

docker kill <containerId/Name>

What is the difference b/w docker stop & docker kill?

docker stop will first send SIGTERM then SIGKILL it will kill process with grace period. Docker kill send SIGKILL it will kill process with out any grace period.



Can we have/run more than one process in a container?
Yes Can we have. But it's not suggestable. 


# Pause contaier process.

docker pause <containerId/Name>

docker unpuase <containerId/Name>

Inspect container
docker inspect <containerId/Name>
docker container inspect <containerId/Name>


It will  container if it is stopped.
docker rm  <containerId/Name>

Force Remove If container is runing we can force remove
docker rm -f <containerId/Name>


How to delete only stopped containers
docker rm $(docker ps -aq --filter  status="exited")

How to delete all containers
docker rm -f $(docker ps -aq)



# How to trouble shoot or debug application which is running as a container?

check if that container is up and running

check if you can access that application locally in docker host server

curl localhost:8080/maven-web-application/

If it is an API or web based application we test locally as 

curl -v localhost:9090/maven-web-application.

docker exec <containerId> ps -ef           (It will check process info of Container ps -ef is used to check process info)

docker exec mavenwebbapp pwd

docker exec -it <containerId/Name> /bin/bash or sh

Go inside of container curl -v localhost:8080/maven-web-application/
if any response no issues..here

docker logs <containerId/Name>
docker logs --tail <NoOflines> <containerId/Name>
docker logs -f <containerId/Name>                    (Floating logs, Uppending New logs)

docker container inspect <containerId/Name>

# If the container is deleted and recreated does the data, files, folders retains?
No....But softwares are created and copied while creating an image those will retain and further actions and changes wont be there untill a backup is taken..

# It will display process details which is runing inside a container.
docker top <containerId/Name>

docker stats <containerId/Name>

# It will display resource(RAM,CPU) consumtion details.
docker stats <containerId/Name>

# Execute commands on a runinging container.
docker exec <containerId/Name> <cmd>

ex:
docker exec javawebapp ls
docker exec javawebapp pwd

How to go inside a container?

docker exec -it <containerId/Name> /bin/bash
 
       or

docker exec -it <containerId/Name> /bin/sh

# Docker attach will attach container process or shell to host server
docker attach <containerId/Name>

If we have to come out with out stoping the process cntl p+q.

# How to copy files from container to host system or host system to container?

docker cp

Container to the system

docker cp <containerName>:</pathOftheContainerFile>  <SystemPath>/<fileName>

docker cp javawebappone:/usr/local/tomcat/logs/catalina.2020-04-23.log  javawebappone.log

system to the Container 

docker cp  <SystemPath>/<fileName><containerName>:</pathOftheContainerFile> 

docker cp  /home/ubunut/test.log javawebappone:/usr/local/tomcat/logs/test.log

docker rename <ContainerId/NameOld> <NewName>

What is difference b/w docker cp & COPY?

# What is docker commit?
Using docker commit we can create image from the continer.

docker commit <containerId/Name> <imageName>

# Can we set CPU,RAM limit for the containers while creating?
Yes We set using options while creating a container.

docker run -d --name <containerName>  --cpus="1" --memory="1g" -p <hostPort>:<containerPort> <imageName>

ex:
docker run --name javawebapp -d --cpus="0.25" --memory="256m"   -p 7070:8080 dockerhandson/java-web-application:1

But cannot set limits after creating a container....

# Can we run multiple Process applications inside of a single container?
yes it is technically possible, But it is not recommended as whole containrization concept is to Isolate the Application..


# What is Docker Image

DockerImage --> It's package which contains application code + all it's dependencies(Software+ENV Varibles + Config Files) together.

EX:

FROM tomcat:8.0.20-jre8
COPY target/java-web-app*.war /usr/local/tomcat/webapps/java-web-app.war





# Dockerfile keywords
===================

FROM

MAINTAINER

COPY

ADD

RUN

CMD

ENTRYPOINT

WORKDIR

ENV

EXPOSE

USER

VOLUME

LABEL

ARG



FROM --> FROM indicates the image base image which we are using to build our own image.All sub sequent instructions will be executed on top of base image
layers.


Syntax: 
FROM  <ImageName>

Ex:

FROM tomcat:8.0.20-jre8(Software)

FROM openjdk:8-alpine


MAINTAINER --> It's will be used as commnets to describe author/owner who is maintaning docker file.

MAINTAINER MithunTech <devopstrainingblr@gmail.com>


COPY --> Using COPY we can copy files/folders to the image. Files/Folders will be copied while creating an image.
It will copy local files from host server(docker server build context)from where we are building image to the image while creating a image.

SYTNAX:
======
COPY <source>                <destination> 
      ServerFile/FolderPath   PathInsideImage
EX:
COPY target/java-web-app.war /usr/local/tomcat/webapps/java-web-app.war

# Below also valid it will copy all the files/folder from HOST Machine current working
directory to Image working dirctroy.
COPY . .

ADD --> ADD also can copy files to the image while creating image. ADD can copy local files from host server(build context) and also it can download files from remote HTTP/S locations while creating a image.
		
ADD <URL> <destination>

ADD <source> <destination>

EX:

# File from http(s) location
ADD https://downloads.apache.org/tomcat/tomcat-8/v8.5.54/bin/apache-tomcat-8.5.54.zip /opt/ 

# Local file
ADD target/java-web-app.war  /usr/local/tomcat/webapps/java-web-app.war

Note: If it's tar file ADD will copy file and also it will extract tar file.

RUN ,CMD, ENTRYPOINT instruncations can be used to execute commands.

RUN --> RUN instruncation  will  execute commands .RUN commands or instructions will be executed while creating an image on top of the previous layers(Image). Next to run you can mention any command based on base os of image.We can have n number RUN instructions in a docker file all the RUN instructions will be exectued one after the other from top to bottom.

Syntax: 
#Shell Form
RUN <commond with args> 
#Executable Form
RUN ["commond" , "Arg1","Arg2"]

EX:
RUN mkdir -p /opt/app				
RUN tar -xvzf /opt/apache-tomcat-8.5.54.tar.gz 


CMD  --> CMD instruncation will execute commands. CMD commands or instructions will be executed while creating a container.CMD insturction can be used to start the process inside the container.

#Shell Form
CMD <commond with args> 
#Executable Form
CMD ["commond" , "Arg1","Arg2"]

# Shell Form
CMD java -jar springapplication.jar. 
# Executable form
CMD ["java", "-jar" , "springapplication.jar"] 


What is difference b/w RUN & CMD?

RUN instructions will be executed while creating a image. CMD Instructions will be executed while creating a
container.We can have more than one RUN keyword in a docker file. All the RUN keywords will be processed while creating an image in the defined order(top to bottom).

Can we have more than one CMD in dockerfile?
Yes you can have. But only the last one/recent one in the order will be proccessed while creating a container.


ENTRYPOINT --> ENTRYPOINT configures a container that will run as an executable.ENTRYPOINT is a command or script that is executed when you run the docker container.


#Shell Form
ENTRYPOINT <commond with args> 
#Executable Form
ENTRYPOINT ["commond" , "Arg1","Arg2"]


Can we have both CMD & ENTRYPOINT in docker file? 

Yes we can have both in a docker file. CMD instructions will not be executed if we have both CMD & ENTRYPOINT.CMD instructions will be passed as an arguments for ENTRYPOINT.

FOR Example:
CMD ls
ENTRYPOINT ["echo", "Hello"]

IT Will be executed as below
/bin/echo HELLO ls 

# Out Put
Hello ls

Requirement always we have to execute sh catalina.sh . But argument by default it has to execute "start". But dynamically i should a option to pass different argument while creating a container.

CMD start
ENTRYPOINT ["sh", "catalina.sh"]


Shell vs Exec form From
EXEC:
<instruction> ["executable", "param1", "param2", ...]

When the exec form of the CMD instruction is used the command will be executed without a shell.

CMD ["executable","param1","param2"]

This is the preferred form for CMD and ENTRYPOINT instructions.
Whether you’re using ENTRYPOINT or CMD (or both) the recommendation is to always use the exec form so that, it’s obvious which command is running as PID 1 inside your container and it can listen to SIGNALS.

Examples:
FROM ubuntu:trusty  
CMD ["/bin/ping","localhost"]


Examples:
FROM ubuntu:trusty  
ENTRYPOINT ["/bin/ping","localhost"]

When instruction is executed in exec form it calls executable directly, and shell processing does not happen.
For example, the following snippet in Dockerfile-
ENV name John Doe 
ENTRYPOINT ["/bin/echo", "Hello, $name"]

When the container runs as docker run -it <image> , it will produce output- Hello, $name
Note that the variable name is not substituted.

SHELL form-
<instruction> <command>
CMD executable param1 param2

When using the shell form, the specified binary is executed with an invocation of the shell using /bin/sh -c

Examples:
FROM ubuntu:trusty 
ENTRYPOINT echo "Hello world"


FROM ubuntu:trusty 
CMD echo "Hello world"

When instruction is executed in shell form it calls /bin/sh -c <command> under the hood and normal shell processing happens.



ENV --> ENV instruction sets the environment variable and this sets the environment for the subsequent build instructions. It takes two forms: one with a single variableENV <key> <value> and another with multiple variables ENV <key> =<avlue> <key> = <value>.



ARG -> ARG Instruction defines a variable that can be passed at build time. Once it is defined in the Dockerfile you can pass with this flag --build-arg while building the image. We can have multiple ARG instruction in the Dockerfile. ARG is the only instruction that can precede the FROM instruction in the Dockerfile.

ARG values are not available after the image is built. A running container won’t have access to an ARG variable value


EX:

ARG TAG=latest
FROM centos:$TAG
docker build -t <image-name>:<tag> --build-arg TAG=centos8 .



WORKDIR --> WORKDIR  is used to define the working directory of a Docker container at any given time. The command is specified in the Dockerfile.It is optional (default is / , but base image might have set it), but considered a good practice. Subsequent instructions in the Dockerfile, such as RUN , CMD and ENTRYPOINT will operate in this dir.

Ex:

WORKDIR /app



USER 

The USER instruction sets the user name (or UID) and optionally the user group (or GID) to use when running the image and for any RUN, CMD and ENTRYPOINT instructions that follow it in the Dockerfile


LABEL

The LABEL instruction adds metadata to an image. A LABEL is a key-value pair. To include spaces within a LABEL value, use quotes and backslashes as you would in command-line parsing. A few usage examples:


LABEL branch=develop

LABEL description="This text illustrates"


An image can have more than one label. You can specify multiple labels on a single line.

LABEL label1="value1" label2="value2" other="value3"
  
  
EXPOSE

The EXPOSE instruction informs Docker that the container listens on the specified network ports at runtime.

The EXPOSE instruction does not actually publish the port. It functions as a type of documentation between the person who builds the image and the person who runs the container, about which ports are intended to be published. To actually publish the port when running the container, use the -p flag on docker run to publish and map one or more ports.

EXPOSE 8080




Multi Stage Docker file
======================

Multi-stage Docker builds let you write Dockerfiles with multiple FROM statements. This means you can create images which derive from several bases, which can help cut the size of your final build.

Docker images are created by selecting a base image using the FROM statement. You then add layers to that image by adding commands to your Dockerfile.

With multi-stage builds, you can split your Dockerfile into multiple sections. Each stage has its own FROM statement so you can involve more than one image in your builds. Stages are built sequentially and can reference their predecessors, so you can copy the output of one layer into the next.

Example
=======
#Maven
FROM maven:3.5-jdk-8-alpine as build
WORKDIR /app
COPY . .
RUN mvn install

#Tomcat
FROM tomcat:8.0.20-jre8
COPY --from=build /app/target/maven-web-application*.war /usr/local/tomcat/webapps/maven-web-application.war




Best Practices to Follow While Creating Docker Image & Files
-----------------------------------------------------------

1) Use Alpine base images where ever it's possible.
2) Don't install/have un necassary packages(Softwares) & Con't
   copy un necassary files .
3) Don't run container process as root user.Start container
   process(Application) as non root user.  
4) Try to reduce the number layers of image as much as possible.
5) Try to Scan images for fulnerabilites(Cair/Anchor or Inbuilt Scaning in ECR/GCR/ACR).
6) Try to use multi Stage Docker files to reduce size of the image.





  
# Create ECR in AWS.
  
Note: Replcae your ECR URL when with 935840844891.dkr.ecr.ap-south-1.amazonaws.com when u create and push.
ECR
===
docker build -t 935840844891.dkr.ecr.ap-south-1.amazonaws.com/maven-web-app:1

Note: Create IAM Role with required policy and attach to EC2 Servers.

# IAM Policiy to autheticate and pull & Push image.
AmazonEC2ContainerRegistryFullAccess

# IAM Policiy to autheticate and pull image.
AmazonEC2ContainerRegistryReadOnly


# Authentication with ECR
aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 935840844891.dkr.ecr.ap-south-1.amazonaws.com  


# Push Image to ECR

docker push 935840844891.dkr.ecr.ap-south-1.amazonaws.com/maven-web-app:1







# Docker Networks

What is network ?
Group of servers/devices connected to each other in a specific network. If Servers
are in same network each one can talk to another server.

Docker network

If One Container has to talk to another Container in Docker. Both has to created under
same docker network.

If Containers are in two different networks. They can't accees each other.


In which docker network the container will be created if we don't mention network name while
creating a container ?

Containers will be created in a default bridge network.
If we don't mention network name while creating a container.

How to list networks in docker?

docker network ls

Docker will have 3 networks by default.
bridge(default)
host
none/null


docker run -d --name javawebapp -p 8080:8080 dockerhandson/java-web-app

docker run -d --name mavenwebapp dockerhandson/maven-web-app


If containers are created in a default bridge network. Communcation will happen only
with IP Address of container. Communcation will not happen using containerName(hostName).

To Check Go inside javawebapp container and ping mavenwebapp container using name & ip. When we ping using ip it will work it will not able to communicate using name.


Developers should not code the connectivity based on the IP in case of contianers. Since IP address of cotnainers will be dynamic.
IP will keep changing.


How to create a custom bridge network ?

# Create Network
Syntax: docker network create -d <driver> <networkName>

Ex: 
docker network create -d bridge flipkartnetwork

# Inspect network
docker network inspect <networkNameOrId>

If containers are created in custom bridge network. Each container can access other using containerName/ContainerIP.

# Delete Containers which are running in default bridge or create container with different name.

docker run -d --name javawebapp -p 8080:8080  --network flipkartnetwork dockerhandson/java-web-app

docker run -d --name mavenwebapp  --network flipkartnetwork dockerhandson/maven-web-app

Create both containers in same network and try to ping mongo contaner with name & IP  from sprinapp container or vice versa it will work with both.



# Remove unused networks
docker network prune 

# Remove Network
docker network rm <networkNameOrId>

Docker Host Network.

If we create contaienrs in host network. Container will not have IP Address. Container will be created
in a system network.

But we can't create more than one cotnainer with same container port in host network.We no need to do port publish to access
containers.


Docker none/null network

If we create contaienrs in none/null network. Container will not have IP Address.We can't 
accees these contianers from out side or from any other cotnainer.


We connect container to more than one network by using docker connect.

docker network connect <networkName/Id>  <containerName/Id>

docker network disconnect <networkName/Id>  <containerName/Id>







Another Application

Ex: 
docker network create -d bridge springappbridge

# Create Network if not exists
docker run -d --name mongo -e MONGO_INITDB_ROOT_USERNAME=devdb -e MONGO_INITDB_ROOT_PASSWORD=devdb@123  --network springappbridge mongo

docker run -d -p 8080:8080 --name springapp  -e MONGO_DB_HOSTNAME=mongo -e MONGO_DB_USERNAME=devdb -e MONGO_DB_PASSWORD=devdb@123 --network springappbridge  dockerhandson/spring-boot-mongo:1








Docker Volumes
============

Docker containers are used to run applications in an isolated environment. By default, all the changes(data) inside the container are lost when the container is removed/recreated. If we want to keep data between runs, Docker volumes and bind mounts can help. 

Docker volumes are file systems mounted on Docker containers to preserve data generated by the running container.


 Create docker network using below commond(If it's not created already)

     docker network create  -d bridge springappbridge

  Create a mongo contianer with out volume in above network
	 	 
	 docker run -d --name mongo -e MONGO_INITDB_ROOT_USERNAME=devdb -e MONGO_INITDB_ROOT_PASSWORD=devdb@123  --network springappbridge mongo

 Create Spring Application Container in above network & which will talk to mongo data base container

       docker run -d -p 8080:8080 --name springapp  -e MONGO_DB_HOSTNAME=mongo -e MONGO_DB_USERNAME=devdb -e MONGO_DB_PASSWORD=devdb@123 --network springappbridge dockerhandson/spring-boot-mongo
    
	 
 Access Spring application & insert data it will be inserted to mongo db. Delete and recreate mongo container 
   what ever you have inserted will no longer be availbale. As once we delete contaienr data also will be deleted
   in container.
   
   To take maitain state (date) of container we have to use volumes
   
   
   
Bind Mounts:
============


Bind mounts may be stored anywhere on the host system. They may even be important system files or directories. Non-Docker processes on the Docker host or a Docker container can modify them at any time.

Bind mounts may be stored anywhere on the host system. They may even be important system files or directories. Non-Docker processes on the Docker host or a Docker container can modify them at any time.


# Volumes Using bind mount
mkdir mongodbdata(If not exists)
# Delete container if exists then create
docker run -d --name mongo -v /home/ubuntu/mongodbdata:/data/db  -e MONGO_INITDB_ROOT_USERNAME=devdb -e MONGO_INITDB_ROOT_PASSWORD=devdb@123  --network springappbridge mongo






Docker Peristent Volumes(Docker Volumes)
========================================

Volumes are the preferred mechanism for persisting data generated by and used by Docker containers. While bind mounts are dependent on the directory structure and OS of the host machine, volumes are completely managed by Docker. Volumes have several advantages over bind mounts:

Volumes are easier to back up or migrate than bind mounts.
You can manage volumes using Docker CLI commands.
Volume drivers let you provsion volumes on remote hosts or cloud providers.

Volumes are stored in a part of the host filesystem which is managed by Docker (/var/lib/docker/volumes/ on Linux).
Non-Docker processes should not modify this part of the filesystem. Volumes are the best way to persist data in Docker.






# To list volumes
docker volume ls
	 
create a volume a Local Volume(Execute docker volume ls to check existing volumes)

docker volume create mongodb
	
   
 Use above volume while creating container.

     docker run -d --name mongo -v mongodb:/data/db   -e MONGO_INITDB_ROOT_USERNAME=devdb -e MONGO_INITDB_ROOT_PASSWORD=devdb1234  --network springappnetwork mongo
   
Access Spring application & insert data it will be inserted to mongo db. Delete and recreate mongo container with same volume mapping. You can see the data back.
   
   
   
Volume Driver Plugin --> It's a piece of code or software which is responsible for creating a storage and attaching the storage to the container.   
    
 ===== Network Volumes Using AWS EBS==========
 
 1) Create IAM User with EC2 Full Access and user access key & Secret Key of the same. Replace your access key & secret below. Or Use Your root aws account access Key & Secret Key.

 docker plugin install rexray/ebs EBS_ACCESSKEY=<ACCESSKEY> EBS_SECRETKEY=<SECRETKEY>
 
 EX:
 
 docker plugin install rexray/ebs EBS_ACCESSKEY=AKIAJRVS26WY3UKXG57Q EBS_SECRETKEY=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

 docker volume create --driver rexray/ebs --name ebsvolume

 docker run -d -p 27017:27017 -v ebsvolume:/data/db  --name mongo -e MONGO_INITDB_ROOT_USERNAME=devdb -e MONGO_INITDB_ROOT_PASSWORD=devdb1234  --network springappnetwork mongo


Map Volumes As Read Only using below option>
-v <volumeName/BindMount>:<containerPath>:ro





Docker Compose
==============

Docker Compose is a tool for defining and running multicontainer applications.


With out compose to deploy above applications which has only 2 images we executed below commnads.


docker network create -d bridge springappnetwork

docker volume create -d local mongobkp

 docker run -d --name mongo -v mongobkp:/data/db -e MONGO_INITDB_ROOT_USERNAME=devdb -e MONGO_INITDB_ROOT_PASSWORD=devdb1234  --network springappnetwork mongo
 
 docker run -d -p 8080:8080 --name springapp  -e MONGO_DB_HOSTNAME=mongo -e MONGO_DB_USERNAME=devdb -e MONGO_DB_PASSWORD=devdb1234 --network springappnetwork dockerhandson/spring-boot-mongo
 

With Docker Compose we deploy/create all of the above 4 with single command using compose file.


With Compose

Install docker compose using below command:

sudo apt install docker-compose

We will define all the serivces(cotainers) details in compose file using compose file we can deploy multi container applications.

Defautl name : docker-compose.yml or docker-compose.yaml


Example 1: (Volumes & Networks also will be created by docker compose)


version: '3.1'
services:
  springboot:
    image: dockerhandson/spring-boot-mongo:latest
    restart: always # This will be ignored if we deploy in docker swarm
    container_name: springboot
    environment:
    - MONGO_DB_HOSTNAME=mongo
    - MONGO_DB_USERNAME=devdb
    - MONGO_DB_PASSWORD=devdb@123
    ports:
      - 8080:8080
    working_dir: /opt/app
    depends_on:
      - mongo
    deploy:  # This will be considered only in docker swarm.
      replicas: 2
      update_config:
        parallelism: 1
        delay: 20s
      restart_policy:
        condition: on-failure
        delay: 10s
        max_attempts: 5
    networks:
    - springappnetwork
  mongo:
    image: mongo
    container_name: springboot-mongo
    environment:
    - MONGO_INITDB_ROOT_USERNAME=devdb
    - MONGO_INITDB_ROOT_PASSWORD=devdb@123
    volumes:
      - mongodbvol:/data/db
    restart: always
    networks:
    - springappnetwork
    
volumes:
  mongodbvol:
    driver: local

    
networks:
  springappnetwork:
    driver: bridge
    
    


 
Commands
# Syntax Check
docker-compose config 
# Create Services/Contianers
docker-compose up -d  
  
# Remove Services/Contianers 
docker-compose down


Example 2: (Volumes & Networks will not be created by docker compose.As we set volumes and networks as external)
==========
 
version: '3.1'

services:
  springboot:
    image: dockerhandson/spring-boot-mongo:latest
    restart: always # This will be ignored if we deploy in docker swarm
    container_name: springboot
    environment:
    - MONGO_DB_HOSTNAME=mongo
    - MONGO_DB_USERNAME=devdb
    - MONGO_DB_PASSWORD=devdb1234
    ports:
      - 8080:8080
    working_dir: /opt/app
    depends_on:
    - mongo
    deploy:  # This will be considered only in docker swarm.
      replicas: 2
      update_config:
        parallelism: 1
        delay: 20s
      restart_policy:
        condition: on-failure
        delay: 10s
        max_attempts: 5
    networks:
    - flipkartnetwork
  mongo:
    image: mongo
    container_name: springboot-mongo
    environment:
    - MONGO_INITDB_ROOT_USERNAME=devdb
    - MONGO_INITDB_ROOT_PASSWORD=devdb1234
    volumes:
      - mongodb:/data/db
    restart: always
    networks:
    - flipkartnetwork
    
volumes:
  mongodb:
    external: true
    
networks:
  flipkartnetwork:
    external: true
	
	
If docker compose file with custom name.	
docker-compose -f <CustomeComposeFileName>.yml <command>

Ex:
docker-compose -f docker-compose-springapp.yml config
docker-compose -f docker-compose-springapp.yml up -d

docker-compose -f docker-compose-springapp.yml down

docker-compose help

Docker Compose Commands:

  config             Validate and view the Compose file
  create             Create services
  down               Stop and remove containers, networks, images, and volumes
  exec               Execute a command in a running container
  help               Get help on a command
  images             List images
  kill               Kill containers
  logs               View output from containers
  pause              Pause services
  port               Print the public port for a port binding
  ps                 List containers
  pull               Pull service images
  push               Push service images
  restart            Restart services
  rm                 Remove stopped containers
  run                Run a one-off command
  scale              Set number of containers for a service
  start              Start services
  stop               Stop services
  top                Display the running processes
  unpause            Unpause services
  up                 Create and start containers
  version            Show the Docker-Compose version information 
  


# In Normal(Standalone) Docker Server We can use below command to create a containers.
docker-compose up

# In docker swarm we will use below command to deploy services using docker compose.
docker stack deploy --compose-file docker-compose.yml <stackName>




Containerization Tools: docker,rocker(rkt),coreos

Container Orchestration Tools: docker swarm,kubernetes,openshift ..etc



H.A --> HighAvailability
F.T --> Fault Tolarence
Scalability
L.B




Create 3 Ubuntu Linux Systems in AWS Execute following commands 

#!/bin/bash
sudo apt-get update
sudo apt-get install curl -y
sudo curl -fsSL get.docksal.io | bash
sudo usermod -aG docker ubuntu

Logout from the the terminal and login again

Note: Make Sure You Open Required/All Ports in AWS Security Groups.

======================================================================
# Initialize docker swarm cluster by exeuting below command on docker server which you want make it as Manager

docker swarm init 

# Initialyze Docker swarm with Public IP
Note: Don't use below(If restart your systems public ip will change will break your cluster) use above commond to initilaze cluster.

docker swarm init  --listen-addr=eth0 --advertise-addr $(curl http://169.254.169.254/latest/meta-data/public-ipv4) (Only run in manager node)



docker swarm join-token worker (Get the token in manager & exeute in nodes)

docker swarm join-token master (Get the master token in manager & exeute in nodes which u want to join cluster as managers)

======================================================================




Docker Swarm has two modes

Global   --> All the nodes (3 servers 1 Manager + 2 Workers)
Replicas --> It will deploye based on replicated number.



What is serivce in docker or docker swarm?

Serivce is nothing but a collection of one or more replicas(contianers) of same type(Image).


What is stack in docker or docker swarm?

Stack is nothing but a collection of one or more serivces of some application.

# Default Mode Replica and it will create a service with 1 replica
docker service create  -p 8080:8080 --name javawebapp dockerhandson/java-web-app

docker service ls

docker service ps <servcieNAme>
ex:
docker service ps javawebapp

docker service scale <serviceName>=<noOfReplicas>
docker service scale javawebapp=3

docker service scale javawebapp=2


# While creating service we can mention number of replicas as below
docker service create  -p 5000:5000 --name pythonapp --replicas 2 dockerhandson/python-flask-app:1

# List contianers running in the given node managed by swarm
docker node ps <nodeName>





# Global Mode
docker service create  --name nginx --mode global   -p 80:80 nginx


#Inspect docker node to check the labels and role of the node

docker node inspect <nodeId/Name>

# User constriants to create containers in specific docker hosts based on condtion(In below Case Containers will be created only in workers)
docker service create  -p 8080:8080 --name javawebapp --replicas 2 --constraint 'node.role==worker' dockerhandson/java-web-app


# Add labels to node
docker node update --label-add key=value <nodeid>
Ex: docker node update --label-add type=appServer qmdh9tgvdef99sryhbezswfl9

#Use above label in constrainsts
docker service create  -p 8080:8080 --name javawebapp --replicas 1 --constraint 'node.labels.type==appServer' dockerhandson/java-web-app

# Drain Nodes in Cluster(Swarm will not create containers in drained nodes)
docker node update --availability drain <NodeID>

# Make Node Active in Cluster
docker node update --availability active <NodeID>


# Create a service with a rolling update policy
docker service create --replicas 2  --name javawebapp  --update-delay 30s --update-parallelism 1  dockerhandson/java-web-app:1

# Update service image without down time.
docker service update --image dockerhandson/java-web-app:2 javawebapp





docker stack deploy --compose-file docker-compose.yml springmongo

docker stack ls

docker stack rm <stackName>

docker stack services <stackName>

docker stack ps <stackName>


version: '3.1'

services:
  springboot:
    image: dockerhandson/spring-boot-mongo:latest
    restart: always # This will be ignored if we deploy in docker swarm
    container_name: springboot
    environment:
    - MONGO_DB_HOSTNAME=mongo
    - MONGO_DB_USERNAME=devdb
    - MONGO_DB_PASSWORD=devdb1234
    ports:
      - 8080:8080
    working_dir: /opt/app
    depends_on:
    - mongo
    deploy:  # This will be considered only in docker swarm.
      replicas: 2
      update_config:
        parallelism: 1
        delay: 20s
      restart_policy:
        condition: on-failure
        delay: 10s
        max_attempts: 5
    networks:
    - flipkartnetwork
  mongo:
    image: mongo
    container_name: springboot-mongo
    environment:
    - MONGO_INITDB_ROOT_USERNAME=devdb
    - MONGO_INITDB_ROOT_PASSWORD=devdb1234
    volumes:
      - mongodb:/data/db
    restart: always
    networks:
    - flipkartnetwork
    
volumes:
  mongodb:
  
    
networks:
  flipkartnetwork:
    external: true


# To come out of swarm execute below commond in worker node
docker swarm leave

# Remove node from Manager
docker node rm <nodename>



# Use private ECR As Private Repo repo's.
#Send registry authentication details to swarm agents using --with-registry-auth	



Create ECR in AWS.
  
Note: Replcae your ECR URL with 935840844891.dkr.ecr.ap-south-1.amazonaws.com when u create and push.
ECR
===
docker build -t 935840844891.dkr.ecr.ap-south-1.amazonaws.com/maven-web-app

# Authentication with ECR(Install AWS CLI And execute below command after attaching IAM Role)
aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 935840844891.dkr.ecr.ap-south-1.amazonaws.com  


Note: Create IAM Role with required policy and attach to EC2 Servers.

# IAM Policiy to autheticate and pull & Push image.
AmazonEC2ContainerRegistryFullAccess

# IAM Policiy to autheticate and pull image.
AmazonEC2ContainerRegistryReadOnly


#While Creating a Service Or Stack send registry authentication details to swarm agents using --with-registry-auth	
	
docker service create  -p <hostPort>:<containerPort> --name <serviceName> --replicas 1  --with-registry-auth <imageName>

docker stack deploy --compose-file docker-compose.yml  --with-registry-auth <stackName>


# Some Other docker and Linux commands

docker inspect -format '{{.NetworkSettings.IPAddress}}' mavenwebapp

# How to move from one server to another

docker save and docker load

docker save -o <fileName>.tar <ImageId/Name>    

The Docker save creates a tar file and the tar file creates all the layers of the image

Once the the tar file is created we can scp the tar file to the another server

scp image.tar ubuntu@ip...

AFter copying to another server

docker load -i <filename>.tar

It will load Image out of Tar file....
.......

# Docker cache concept

docker uses cache concept to build the image and recreates and process the layer again, It Is using the concept of build cache 
The advantage of Build cache is to improve the speed while creating a image

/var/lib/docker/Overlay2 in this folder it saves cache of images..

The build cache improves build processing time

If i dont want to use cache while creatinf docker images we can use command as

docker build -t imageone --no-cache

# Docker File in Detail...

Docker file: It is a file where we can define Instructions to create a docker image. Dockerfile is an input to create a image.

Docker daemon will process docker file instructios from top to bottom order.

Default Name: Docker file.

can we have docker file with custom name?
Yes. we can have docker file with custom name. we will use -f option while building docker image

docker build -f <customDockerfileName> <ImageTag> <buildContext>

we will use Docker DSL key words (Instructions/Directives in Dockerfile)

DSL---Domain specific Language


FROM 
MAINTAINER
COPY
AND
RUN
CMD
ENTRYPONT
WORKDIR
ENV
ARG
LABEL
EXPOSE
------------------------
FROM --> FROM indicates the image base image which we are using to build our own image.All sub sequent instructions will be executed on top of base image
layers.


Syntax: 
FROM  <ImageName>

Ex:

FROM tomcat:8.0.20-jre8(Software)

FROM openjdk:8-alpine

FROM <registry/Repo:TAG>

FROM nexus.tcs.com/tomcat:8.2

FROM 20786.........amazon.com/tomcat/8.5

Except ARG we cant have any other instruction as First Instruction before FROM

ARG <KEY>=<VALUE>
FROM <BaseImageName>
-------------------------------


MAINTAINER --> It's will be used as commnets to describe author/owner who is maintaning docker file.

MAINTAINER MithunTech <devopstrainingblr@gmail.com>

It is Kind of Documentation,

-----------------------------------

COPY --> Using COPY we can copy files/folders to the image. Files/Folders will be copied while creating an image.
It Will copy local files from host/local server(docker server build context)from server where we are building image files/folders.

SYTNAX:
======
COPY <source>                <destination> 
      ServerFile/FolderPath   PathInsideImage
EX:
COPY target/java-web-app.war /usr/local/tomcat/webapps/java-web-app.war

# Below also valid it will copy all the files/folder from HOST Machine current working
directory to Image working dirctroy.
COPY . .

we can copy from files/Folders t0 IMAGE also

we can give like this also

COPY . .
First . Indicates Source cureent working directory and second . Indicates second curent working directory of Image.

------------------------------------------------------------------

ADD --> ADD also can copy files to the image while creating image. ADD can copy local files from host server(build context) and also it can download files from remote HTTP/S locations while creating a image.
		
ADD <URL> <destination>

ADD <source> <destination>

EX:

# File from http(s) location
ADD https://downloads.apache.org/tomcat/tomcat-8/v8.5.54/bin/apache-tomcat-8.5.54.zip /opt/ 

# Local file
ADD target/java-web-app.war  /usr/local/tomcat/webapps/java-web-app.war

Note: If it's tar file ADD will copy file and also it will extract tar file.

If the file is tar.gz extension it wont extract

---------------------------------------------------------------------------------

RUN ,CMD, ENTRYPOINT instruncations can be used to execute commands.

RUN --> RUN instruction can be  execute commands .RUN commands or instructions will be executed while creating an image on top of the previous layers(Image). Next to run you can mention any command based on base os of image. We can have n number RUN instructions in a docker file all the RUN instructions will be exectued one after the other from top to bottom.

In simple RUN instruction will be executed inside an image.

Run Instructions can be used to configure(Install) required softwares (packages in the image)

Run Instructions will be executed while creating a image.

Rn mkdir /opt/tomcat
Run apt install git -y
RUN tar -xvzf /opt/tomcat/apache-tomcat-8.5.76.tar.gz
RUN apt install curl -y

Syntax: 
#Shell Form
RUN <commond with args> 
#Executable Form
RUN ["commond" , "Arg1","Arg2"]

EX:
RUN mkdir -p /opt/app				
RUN tar -xvzf /opt/apache-tomcat-8.5.54.tar.gz 

Order is Imp for dependednt Instruction..

Using an RUN Instructions we can run commands while creating a IMAGE........

1phase               2phase          3phase
DOCKERFILE .........IMAGE..........CONTAINER.

-----------------------------------------------------------------------------------------------------------------------------------------------

CMD  --> CMD Instructions will execute commands. CMD commands or instructions will be executed while creating a container.CMD insturction can be used to start the process inside the container.
CMD instructions will be executed While staring a container, CMD Instructions is used to start the application process inside a container.

#Shell Form
CMD <commond with args> 
#Executable Form
CMD ["commond" , "Arg1","Arg2"]

# Shell Form
CMD java -jar springapplication.jar. 
# Executable form
CMD ["java", "-jar" , "springapplication.jar"] 


What is difference b/w RUN & CMD?

RUN instructions will be executed while creating a image. CMD Instructions will be executed while creating a
container.We can have more than one RUN keyword in a docker file. All the RUN keywords will be processed while creating an image in the defined order(top to bottom).

Can we have more than one CMD in dockerfile?
Yes you can have. But only the last one/recent one in the order will be proccessed while creating a container.
Only One CMD will be Executed not all if you have created extra aslo...
....................................................................................................................................................................

ENTRYPOINT --> ENTRYPOINT configures a container that will run as an executable.ENTRYPOINT is a command or script that is executed when you run the docker container.
We can set an entrypoint for our image(container). Using entrypoint also we can execute command or script also gets executed.
This Entry point gets executed when starting a container.


#Shell Form
ENTRYPOINT <commond with args> 
#Executable Form
ENTRYPOINT ["commond" , "Arg1","Arg2"]


Can we have both CMD & ENTRYPOINT in docker file? 

Yes we can have both in a docker file. CMD instructions will not be executed if we have both CMD & ENTRYPOINT. CMD instructions will be passed as an arguments for ENTRYPOINT.

FOR Example:
CMD ls
ENTRYPOINT ["echo", "Hello"]

IT Will be executed as below
/bin/echo HELLO ls 

# Out Put
Hello ls

Requirement always we have to execute sh catalina.sh . But argument by default it has to execute "start". But dynamically i should a option to pass different argument while creating a container.

CMD start
ENTRYPOINT ["sh", "catalina.sh"]


Shell vs Exec form From
EXEC:
<instruction> ["executable", "param1", "param2", ...]

When the exec form of the CMD instruction is used the command will be executed without a shell.

CMD ["executable","param1","param2"]

This is the preferred form for CMD and ENTRYPOINT instructions.
Whether you’re using ENTRYPOINT or CMD (or both) the recommendation is to always use the exec form so that, it’s obvious which command is running as PID 1 inside your container and it can listen to SIGNALS.

Examples:
FROM ubuntu:trusty  
CMD ["/bin/ping","localhost"]


Examples:
FROM ubuntu:trusty  
ENTRYPOINT ["/bin/ping","localhost"]

When instruction is executed in exec form it calls executable directly, and shell processing does not happen.
For example, the following snippet in Dockerfile-
ENV name John Doe 
ENTRYPOINT ["/bin/echo", "Hello, $name"]

When the container runs as docker run -it <image> , it will produce output- Hello, $name
Note that the variable name is not substituted.

SHELL form-
<instruction> <command>
CMD executable param1 param2

When using the shell form, the specified binary is executed with an invocation of the shell using /bin/sh -c

Examples:
FROM ubuntu:trusty 
ENTRYPOINT echo "Hello world"


FROM ubuntu:trusty 
CMD echo "Hello world"

When instruction is executed in shell form it calls /bin/sh -c <command> under the hood and normal shell processing happens.



ENV --> ENV instruction sets the environment variable and this sets the environment for the subsequent build instructions. It takes two forms: one with a single variableENV <key> <value> and another with multiple variables ENV <key> =<avlue> <key> = <value>.



ARG -> ARG Instruction defines a variable that can be passed at build time. Once it is defined in the Dockerfile you can pass with this flag --build-arg while building the image. We can have multiple ARG instruction in the Dockerfile. ARG is the only instruction that can precede the FROM instruction in the Dockerfile.

ARG values are not available after the image is built. A running container won’t have access to an ARG variable value


EX:

ARG TAG=latest
FROM centos:$TAG
docker build -t <image-name>:<tag> --build-arg TAG=centos8 .



WORKDIR --> WORKDIR  is used to define the working directory of a Docker container at any given time. The command is specified in the Dockerfile.It is optional (default is / , but base image might have set it), but considered a good practice. Subsequent instructions in the Dockerfile, such as RUN , CMD and ENTRYPOINT will operate in this dir.

Ex:

WORKDIR /app



USER 

The USER instruction sets the user name (or UID) and optionally the user group (or GID) to use when running the image and for any RUN, CMD and ENTRYPOINT instructions that follow it in the Dockerfile


LABEL

The LABEL instruction adds metadata to an image. A LABEL is a key-value pair. To include spaces within a LABEL value, use quotes and backslashes as you would in command-line parsing. A few usage examples:


LABEL branch=develop

LABEL description="This text illustrates"


An image can have more than one label. You can specify multiple labels on a single line.

LABEL label1="value1" label2="value2" other="value3"
  
  
EXPOSE

The EXPOSE instruction informs Docker that the container listens on the specified network ports at runtime.

The EXPOSE instruction does not actually publish the port. It functions as a type of documentation between the person who builds the image and the person who runs the container, about which ports are intended to be published. To actually publish the port when running the container, use the -p flag on docker run to publish and map one or more ports.

EXPOSE 8080




Multi Stage Docker file
======================

Multi-stage Docker builds let you write Dockerfiles with multiple FROM statements. This means you can create images which derive from several bases, which can help cut the size of your final build.

Docker images are created by selecting a base image using the FROM statement. You then add layers to that image by adding commands to your Dockerfile.

With multi-stage builds, you can split your Dockerfile into multiple sections. Each stage has its own FROM statement so you can involve more than one image in your builds. Stages are built sequentially and can reference their predecessors, so you can copy the output of one layer into the next.

Example
=======
#Maven
FROM maven:3.5-jdk-8-alpine as build
WORKDIR /app
COPY . .
RUN mvn install

#Tomcat
FROM tomcat:8.0.20-jre8
COPY --from=build /app/target/maven-web-application*.war /usr/local/tomcat/webapps/maven-web-application.war




Best Practices to Follow While Creating Docker Image & Files
-----------------------------------------------------------

1) Use Alpine base images where ever it's possible.
2) Don't install/have un necassary packages(Softwares) & Con't
   copy un necassary files .
3) Don't run container process as root user.Start container
   process(Application) as non root user.  
4) Try to reduce the number layers of image as much as possible.
5) Try to Scan images for fulnerabilites(Cair/Anchor or Inbuilt Scaning in ECR/GCR/ACR).
6) Try to use multi Stage Docker files to reduce size of the image.

........................................................................................................................................................................
# Jenkins and Docker
sudo apt update
sudo apt insatll openjdk... -y

# Install Jenkins

sudo wget -q -o - Jenkins Url | sudo apt-key add -

sudo sh -c 'echo deb Jenkinslink/ > /etc/apt/sources.list.d/jenkins.list'

sudo apt update

sudo apt install jenkins

sudo systemctl status jenkins

# Install docker in Jenkins server
sudo apt install docker.io -y

# Add jenkins user to docker 

sudo usermod -aG docker jenkins

# Restart Jenkins

sudo systemctl restart jenkins

# plugins used in jenkins

ssh Agent

# Install Docker in Deployment server

sudo apt update

sudo apt install docker.io -y

sudo usermod -aG docker jenkins

# CI/CD Job for jenkins docker as pipeline script

node {

  def BuildNumber=BUILD_NUMBER

  stage("Git Clone"){
    git url: 'https://........................, branch: 'master'
  }
  stage("Maven clean Packaage"){
     def maven= tool name: "Maven",type: "maven"
     sh "${mavenHome}/bin/mvn clean package
  }
  stage("SoanrReport"){
    def maven= tool name: "Maven",type: "maven"
    sh "${mavenHome}/bin/mvn sonar:sonar
  }
  stage("Build Docker image"){
    sh "doker build -t dockerhubusername/Java-web-app-Docker:${BuildNumber} ."               Here dot reperesent Docker context path of current docker dir.
  }
  stage("Docker login and Push"){
   withCredentials.........Used Credentials and masked password as variable and code as snippet credentialid: DockerHubPwd', Variable: "DockerHubPwd')})
   sh :docker login -u loginNameofRepo -p ${DockerHubPwd"}
   sh "docker push dockerhubusername/java-web-app-docker:${buildNumber}"
  }
  stage("Deploy Application As Docker Container In docker Deployment server"){
    //Add Credentials and configure docker server private key in jenkins server in Jnekins credentials.
    //ssh agent generate pipeline script
    sshagent([copy and paste the snippet here])
    sh "ssh -o StrictHostKeyChecking=no ubuntu@ip_address docker rm javawebappcontainer | true"
    sh "ssh -o StrictHostKeyChecking=no ubuntu@ip_address docker run -d -p 8080:8080 --name javawebappcontainer <dockerregistryname>/Java-web-app-docker:${buildNumber}"
  }
}


Execute Build Job is done..
........................................................................................................................................................................