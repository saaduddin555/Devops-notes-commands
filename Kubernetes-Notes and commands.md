Kubernetes The Orchestration Tool | Docker swarm is also Orchestration tool
The difference between docker and kubernetes are
In docker we cannot do Autoscalling as we have to do manually | In kubernetes we can do autoscalling of resources automatically like Horizantal and vertical autoscalling.
we can create virtual Boundries like creating namespaces in kubernetes | But not in Docker.
The kubernetes is developed by Google and opensourced by google and Linux foundation Team
The Kubernetes is also called as (K8s)
In docker swarm we call as service | In kubernetes we call as pod

Types of Runtime providers(Containarization software):
Docker 
Rocket
Container-D

In kubernetes we can use any Runtime and create virtualized space called as pod and create docker,rocket,Container-D containers
All three can work as individual runtime as pod and supports multiple runtimes as in kubernetes.
-The Docker swarm doesn't support other Runtimes


###### what are the componets and Architecture of kubernetes:

In Master Server we have following components

Controller or Manager
ETCD Database
API Server
Scheduler

In worker Server we have following components:

Kube-proxy
Kubelet
Docker or containarization engine
and has
PODS inside of container


The Worker servers are connected to master node for communication and interconnected with components

The Heart of Kubernetes server is API server components which helps to communicates from master to worker and all servers including manager

kubelet and docker container are interconnected to POD_container

-We communicate to API server which acts as initermidiate to all communication channel

ETC_database: has all info related to clusture and containers and pods info all created and kill info, How many pods and conatiners are running whole database is stored so that in future if something goes wrong the scheduler automatically fixes everything as it should be bcoz of database comminication with it, Basically it is about containers workers and manager basically all data related to Kubernetes operations, It will be stored as Key as value pair format.

controller Manager: It does to manage the task which is given by the user, all operations are handled by controller manager.
                    It acts as a commander to all nodes
Scheduler: Scheduler does the job given by controller manager of specified information and deployes that to containers.

Kube-Proxy: It has all network related Information, Ip address allocation to containers and maintaining network
Kubelet: It is a commander for worker as same as controller manager for master basically takes commands and requirement and satisfies it

Container Engine: which docker container installed and helps to does the task.

How a communication occurs in Kubernetes:
First a request is sent to

Master:
API SERVER------CONTROLLER/MANAGER----------SCHEDULER-----Again Communicates to API TO Check No of workers available and send request as per requirement---------

Goes To

TO Worker 
-----------Kublet-----------Docker Engine----------Container_pods

Pod is an Virtualized Server which can run containers on it.

If a container or Pod is terminated, It can be recreated but with different ip range.
In docker terminate containers cannot be created automatically and etc database watches the liveness of containers in kubernetes and if any issues it recreates it.

-One Ec2 instance or 1 or more can be master for best pratice and other rest Ec2 instances can be workers for master
In docker concept
-A master node also consist of containers in it 
But where as in kubernetes 
-A masternode doesn't create containers in it, but by using as a TAINT service in kubernetes we can create pods and containers in master also.

# Kubernetes Installation

Methods of Installation:

MINIkube
Kubeadm
KOPS
EKS ctl

Either u can use any method to install kubernetes but our goal is to form a kubernetes clusture

Kops Method:Installation
AWS services in KOPS are going to use
*EC2 Machine
*AWS Linux: The Usage of AWS Linux is, it has inbuilt AWS CLI
*S3 Bucket: TO Store server Information
*Route53:DNS registration private
*IAM Role

In kubernetes we no need to be in master node to do task and communicate, we can be in individual server and communicate with Clusture

# log in to AWS management console
Step (1):
 * Take one EC2 Amezon machine either t2 micro or anyother  
 * connect that server with Mobex Term
 * give name log in AS: ec2-user

 Step (2) Switch to root user;

 * sudo -s
 Step (3) Create Role in AWS:
  ROLE:
  * IAM full access
  * S3 Full access
  * Route 53 Full access
  * ec2 full access

  * in AWS console Go to IAM:
   Create role and attche to the EC2 machine
    1 go to IAM
    2 click on role
    3 create role
    4 click on EC2
    5 click on next:permission
    6 give the access
    7 click on preview
    8 Give the role name
    9 click on create role

Step (4) assign the role to the ec2:
* go to the ec2 machine 
* slect the machine and click on actions and instance setting and attach/replace IAM role
* give the role name and click on apply

Step (5) configure the aws:
* aws configure
#(just enter blank)

* Default region: need to mention eg: us-east-1
* output format: table

step (6) Host the public or private DNS:
 # go to route 53
 # cick on hosted Zones
 # clik on create hosted Zones
 # give the DNS name
 # choose the region name EG: us-east-1
 # choose the VPC
 # click on create

step (7) open below link:
* https://github.com/ValaxyTech/DevOpsDemos/blob/master/Kubernetes/k8s-setup.md

Step (8) Install kubectl:

* curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
*  chmod +x ./kubectl
*  sudo mv ./kubectl /usr/local/bin/kubectl
* mv /usr/local/bin/kubectl /bin/
 #check the kuetl version
 * kubectl version

Step (9) Install kops:
*    curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
*  chmod +x kops-linux-amd64
*  sudo mv kops-linux-amd64 /bin/kops

# check kops version
* kops version

step (10) Create a s3 bucket with private zone name to store the cluster information:

* aws s3 mb s3://shaik.in

# check the s3 bucket list

* aws s3 ls

Step(11) Expose environment variable:

*    export KOPS_STATE_STORE=s3://shaik.in

Step (12) Create sshkeys before creating cluster: you may have tyo enter in to the cluster  node with  this SSH:

*  ssh-keygen

Step (13) Create kubernetes cluster definitions on S3 bucket:

*  kops create cluster --cloud=aws --zones=us-east-1a --name=shaik.in --dns-zone=shaik.in --dns private

# you can specify above which zone you want to create the cluster with the Zone id

Step (14) Finally configure your cluster with:
  * kops update cluster shaik.in --yes
  * kops validate cluster
 * kops update cluster --name shaik.in --yes --admin

(((( you  can see the below output :

Cluster is starting.  It should be ready in a few minutes.

Suggestions:
 * validate cluster: kops validate cluster --wait 10m
 * list nodes: kubectl get nodes --show-labels
 * ssh to the master: ssh -i ~/.ssh/id_rsa ubuntu@api.shaik.in
 * the ubuntu user is specific to Ubuntu. If not using Ubuntu please use the appropriate user based on your OS.
 * read about installing addons at: https://kops.sigs.k8s.io/operations/addons.

))))

# wait for minute and check in ec2 Dash board, you can find master and node got created
# you can check in route 53, s3, ec2 instances

# you can validat the cluster

*  kops validate cluster --wait 10m

Step (15) list of nodes:

*   kubectl get nodes 

Step (16) increase the Worker node or add the worker node:

* kops get ig
* kops edit ig nodes-us-east-1a
* kops update cluster
* kops update cluster --yes

==================================================================


Create first pod with container:::::::::::::::::::::::::::::::

* nano multi_container_pod.yml
# Past the below code inside the yml file

apiVersion: v1
kind: Pod
metadata:
  name: web
  labels:
    tier: front
    app: nginx
    role: ui
spec:
  containers:
    - name: nginx
      image: nginx:stable-alpine
      ports:
        - containerPort: 80


* kubectl apply -f multi_container_pod.yml
*  kubectl get pods
* kubectl logs  web  -c nginx
* kubectl exec -it web  sh  -c nginx  # run this command in inside of the container * hostname * ifconfig

# Command to go inside of the specific pod and container
 * kubectl get pods POD_NAME_HERE -o jsonpath='{.spec.containers[*].name}'

        or 
* kubectl get pods -o=custom-columns=PodName:.metadata.name,Containers:.spec.containers[*].name,Image:.spec.containers[*].image
                        or

* kubectl get pods [pod-name-here] -n [namespace] -o jsonpath='{.spec.containers[*].name}*

                 or
# command to create pod and go inside of the container
* kubectl run -i -t pod name --image=ubuntu


------------------------------------------------
* kubectl describe master
* kubectl describe node
# command to create pod 
* kubectl run web-server --image=nginx


Deploying Nginx container on Kubernetes ------------------------------

* kubectl run web-server --image=nginx --port=80
* kubectl get pods
* kubectl get pods -o wide ( get the more information)

.....................................................................................................................................
What is a Pod ?
""" Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.

A Pod (as in a pod of whales or pea pod) is a group of one or more containers,
 with shared storage and network resources, and a specification for how to run the containers. 
 A Pod's contents are always co-located and co-scheduled, and run in a shared context. 
 A Pod models an application-specific "logical host": it contains one or more application containers which are relatively tightly coupled.
 In non-cloud contexts, applications executed on the same physical or virtual machine are analogous to cloud applications executed on the same logical host."""

 Ways to create pod
 ----------------
 1 Imperative Way
 2 Declarative Way


 (1) imperative Way: Crate pod with command line
  * kubectl run podname --image=nginx:latest

 (2) List of Pods:
   * kubectl get pods

(3) get the details about the perticular pod:
 * kubectl describe pod podname

 (4) get the all information:
  * kubectl get all 

(5) kubectl get pod -o wide
   * Get all details related to pod

----------------------------------------------------------------------------------------------------------------

(2) Declarative way: Create Pod with Yaml file

(1) Need to create yaml file
 * nano shaik.yaml
 #paste the below code inside of yaml file

apiVersion: v1
kind: Pod
metadata:
  name: vote
  labels:
    app: python
    role: vote
    version: v1
spec:
  containers:
    - name: app
      image: schoolofdevops/vote:v1


# command to create pod with yaml file
* kubectl create -f .yaml(need to give the file name)

------------------------------------------------------------

How to create pod with multiple containers ======


* nano shaik.yaml
Past the below code inside of yaml file

apiVersion: v1
kind: Pod
metadata:
  name: web
  labels:
    tier: front
    app: nginx
    role: ui
spec:
  containers:
    - name: nginx
      image: nginx:stable-alpine
      ports:
        - containerPort: 80
          protocol: TCP
      volumeMounts:
        - name: data
          mountPath: /var/www/html-sample-app

    - name: sync
      image: schoolofdevops/sync:v2
      volumeMounts:
        - name: data
          mountPath: /var/www/app

  volumes:
    - name: data
      emptyDir: {}



# Create pod with multiple container with the command line
 * kubectl create -f shaik.yaml

 # get the list of all pods

 * kubectl get pods

 # command to go inside of the container in side of the pod

 
* kubectl exec -it web  sh  -c nginx
* kubectl exec -it web  sh  -c sync
 
========================================================================================

# delete the all pods

*kubectl delete --all pods

# command to delete the specific pod 
* kubectl delete pod podname

# delete all pods in all name spaces

* kubectl delete all --all --all-namespace
........................................................................................................................................

# running Notes for Kubernetes

Yaml Files of Kubernetes and Explanation

Pods.Yaml file:

apiVersion:v1
kind: Pod
metadata: 
 name: webapp
spec:
 containers:
 - name: webapp
   image: image_name_from_docker_hub

This is how a Yaml file is written for Pod 

..................................................................................................................................
Kubectl get all                               (to get pods list of all)

kubectl apply -f first-pod.yml                (To apply a yaml file)

minikube ip                                   (gets ip address of the minikube kubernetes clusture)

kubectl describe pod name_of_pod             (gets info all about pod and gets info and events)

kubectl exec webapp ls                       (Get inside of pod which is named as web app and ls means to list the root directory of that pod)

kubectl -it exec webapp sh

wget http://localhost:80                    (that gonna connect local html and download a file index.html which is hosted on localport)

cat index.html                               (if we cat and see any code it means a webserver is inside and ready)

....................................................................................................................................................
# service

-The name of the service should be Unique and critical to mention properly and should be rembered as we may call it multiple times
-When two services are talking to each other we use the service names

Pods are Isolated and Post are not accessed out of the world, They are isolated with in kubernetes clusture, Pods are designed to be very throw away things
Pods have lifetime, they can regulary die, The can be recreated, we treat pods like cattle, they are short lived lifecycle
service in kubernetes is a long running object which is stable and fixed and long running Pods are configured

With a service we can connect to kubernetes clusture and service will find a suitable pod which can service that request

label : it is a set up of pod key value pairs, we can one or more key value pairs, The app:webapp the key is app and value is webapp

When we write a service we provide called as selector and it is called as series of key value pairs like app:webapp

what happens is here the selector matches the key value pairs with pods if u like to select that pod

It is a complicated mechanism which undergoes inside service and pod to communicate each other

The service runs along with pod automatically and remembers the pod state

-For service it will be selector and for Pod it will be label
-selector= app:webapp   while  label=app:webapp


# Service.yaml file

apiVersion: v1
Kind: Service
metadata:
  name: fleetman-webapp

spec: 
 # This defines which pods are going to be represented by this service 
 # The service becomes a network endpoint for either other services
 # or maybe external users to connect to eg: browser
  
 selector:
   app:webapp
      




























