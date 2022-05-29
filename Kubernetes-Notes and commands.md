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

# Kubernetes Most Used commands:
kubectl get all
kubectl apply -f filename.yaml
kubectl describe pod Name_of_pod
kubectl delete svc name_of_service
kubectl delete pod name_of_pod
kubectl delete pod --all
kubectl delete -f
kubectl describe replicaset webapp
kubectl describe rs webapp

# Rolling update and Rollout

kubectl rollout status deploy name_of_deployment               (This cmd rollout to previous version but need to change version of image in yaml file)
kubectl rollout history deploy name_of_deployment              (This command will give details about rollout history)

(kubectl rollout undo deploy name_of_deployment --to-revision=2 (To check revision enter history cmd and to rollout give revision_no to rollback as seen in cmd)

This command helps to roolout basically without editing yaml file to change image version.)

kubectl rollout undo deploy webapp --to-revision=2


# Namespaces
kubectl get namespace
kubectl get pod
kubectl get po -n kube-system
kubectl get all -n kube-system
kubectl get all -n kube-public
kubectl get pod -n monitoring
kubectl get svc -n monitoring

Note: if we are working in a namespace where the pods are there and aligned to it , we get result
or 
we get error from server, stating the pod or service is not exist
so before 
switch to that particular name space or give namespace in command so that the particular pod of that namespace can be fetched.

kubectl describe svc kube-dns (This is dns service as in regular default namespace mode we cannot view the details)
as Kubernetes segreegate namespaces as by default as
System
public 
default 
so if u want to use system namespace resource switch to it first or describe namespace in command.

kubectl describe svc kube-dns -n kube-system  (Here -n represents namespace of that pod called kube-dns and namespace is kube-system)

# How to get inside of the pod
kubectl exec -it pod_name sh

# cat /etc/resolv.conf        where all DNS configuration files exist 
nslookup helps to look up local DNS names and give it Ip by fetching Ip from DNS service of K8S

eg: nslookup www.google.com
eg: nslookup database          (Here in k8s we have service called database configured with mysql pod and service is database hence, k8s automatically configures ip for that database service linked to that pod name my sql and all DNS enteries will be stored in k8s-DNS Pod which manages all DNS services

As above to look a IP address for a DNS name Database we use command called as nslookup database as it give ip address as Mysql pod)

if we want to access database from webserver
mysql
mysql: not found (by default mysql wont be installed in webserver)
as hence we install client to communicate to database server
apk add mysql-client
After Installation of client we can run commands to connect to database server
TO Connect to database Pod
mysql -h database -u root -p password fleetman
here database is refered as DNS name or else should give IP of that database to communicate, as DNS is inbulit in K8s it will recognise 
-u referes as user as here user is as root and -p is password and password is set as password and name_of_datbase what we gave while creating a database should be given.

# Workloads are also called as 
Pods,replicas,deployment in production.


# To debug a failure pod
kubectl describe pod pod_name
kubectl logs pod_name
kubectl logs -f pod_name

We can assign Environment Variables in Yaml files also, if any env variables doesnt match or wrong defined in yaml as defined in code, Pods might also crash always check same.
The Environment can be locally deployment or Test or production level
always check parameter before deploying an app with developer or src section in code.

# persistence and Volume


# Logs Inspection
Log Inspection is Neccessary part of kubernetes where to find what is happening in kubernetes cluster.

kubectl logs pod_name

When a Pod gets restarted all of the logs present in that container will be discarded and hence we need to architect a infrastructure to capture logs for that kubernetes cluster.

The logs helps us to find out the error of Kubernetes pods or cluster

ELK stack is also called as elasticStack, The Stack which helps to collect,store,analyse the logs.
The three major components of distributing loging system are: 

1. Logstash or Fluentd is same as Logstash the both are same which is installed in node to pull all logs of the container
Fluentd is has large range and support for data containers. The job of both is to collect data

2. Elastic search: Elastic search is distributed and Restful search and analytics engine capable of solving a growing number of use cases, As a heart Elastic stack, it centrally stores your data so that you can discover the unexpected and uncover the the unexpected.

3. Kibana: kibana allows to visualize the data such as charts, graphs and bars and get detailed analysis of logs.

In AWS we have elastic search service, instead of putting any where in cluster.

Elastic search shoud be replica set in clusture, atleast two nodes.as it is imp node as it fails it doesnt capture the logs and stores.

Kibana can be installed in single node as it is just front end to explore

we have docker images for all three.


# Types of Services and Methods in Kubernetes

Pod
Replicaset
Deployment
service
Namespaces:
Service Account: 
Cluster role:
Daemon set: It is like a replica set, This deamon set know this needs to know it should be run in every node.
cluster role binding:
StatefulSet 
Nodeport
clusterip
loadbalancer
Request and Limits
Horizantal Pod Autoscaling
Readiness and Liveess prob
Role base access control
Jobs
Ingress control


# Prometheus and Grafana

Cloud watch Alarams may charge in AWS for detailed monitoring hence we use Prometheus and Grafana Externally 
It is Open source and hence it is core part of Kubernetes 
it helps in gathering metrics in prometheus
The graphical tool we choose is called as grafana for analytics and vsiualization.
It is similar like ELK stack

Install Prometheus and Grafana Using helm find out how to use by visiting website helm.sh or Visit github helm repo.

* Prometheus-Operator is a complete monitoring solution combined with prometheus,grafana and Alerting.
  Use prometheus chart to install the stack
  helm install --name Monitoring stable/prometheus-operator

we can edit a pod which is installed by default using Helm by command
kubectl edit -n monitoring service/monitoring-prometheus-oper-prometheus

we can change deafult editor with this command with ENV variable.
export EDITOR=nano

If you have any issues like username and password by default the helm repository contains all info and methods to work.

# How to edit a pod or service Configuration by using command
  
Kubectl edit -n monitoring (service/monitoring-prometheus-oper-prometheus)     

Name of service is given which is shown in brackets, dont use brackets in real time and copy and paste the service which u woud like to edit.

# Alerting

# Using loadbalencer domain name we can get access to various internal pods which are in cluster ip by using proxy method.

The details will differ from browser to browser 

Security of end point using Authentication to access the details of load balancer

Only kubernetes Admins has access to Username and password details

To Find it

Kubectl config view --minify

You will see Autogenerated password.

The result of endpoint is generated.

https://Loadbalancer_domain_name/api/v1/namespaces/monitoring/services/alertmanager-operated:enter_port_number/proxy

The REST interface returns json data in this Link

Even if the service is not exposed still we can access it using cluster admin and password.

The Internal services can be accessed using the method like eg:
Access a web application 

https://Load_balancer_domain_name_which one of service is exposed/api/v1/namespaces/default/services_fleetman_webapp:Portno/proxy

If the application which is dependent up on other services might create an issue viewing it.

watch dog is also called as dead man switches which created alerts to users....

Deadman switch meant to ensure that the entire Alerting pipeline is functional

The Alarm is sound untill the issue is resolved and comes back to normal

The Deadman switch is alert which never be resolved 

Insufficient members

Node disk running full

The Alerts can be redirected to slack channel who can monitor by using emails or txt messages

# requests and Limits




































