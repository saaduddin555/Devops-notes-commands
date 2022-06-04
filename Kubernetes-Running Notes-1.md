Containerization --> Docker, Rocket(Rkt),Container-d
Container Orchestration Tools --> Docker Swarm,Kubernetes,OpenShift


Installation
============

Self Managed K8's Cluster
 minikube --> Single Node K8's Cluster.
 kubeadm --> We can setup multi node k8's cluster using kubeadm.


Cloud Managed(Managed Services)
EKS --> Elastic Kubernetes Service(AWS)
AKS --> Azure Kubernetes Service(Azure)
GKE --> Google Kubernetes Engine(GCP)

KOPS --> Kubernetes Operations is a sotware using which we can create production ready
highily available kubenetes services in Cloud like AWS.KOPS will leverage Cloud Sevices like
AWS AutoScaling & Lanuch Configurations to setup K8's Master & Workers. It will Create 2 ASG & Lanuch Configs
one for master and one for worekrs. Thesse Auto Scaling Groups will manage EC2 Instances.

https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-strong-getting-started-strong-


Name Spaces

kubectl get namespaces

# Create Name Space Using Imperative Command

kubectl create namespace <nameSpaceName>

ex:
kubectl create test-ns


# Using Declarative Manifest file

apiVersion: v1
kind: Namespace
metadata:
 name: <NameSpaceName>
 lables:           # Labels are key value pairs(Metadata)
   <key>: <value>
   <key>  <value>

# Example   
apiVersion: v1
kind: Namespace
metadata:
  name: test-ns
  labels:
    team: qateam

# Command to apply  
kubectl apply -f <fileName>.yaml

kubectl apply -f test-ns.yaml


# Create POD Using Command

kubectl run <podName> --image=<imageName> --port=<containerPort> -n <namespaceName>

ex:
# If we don't mention name space it will create in default(current) namespace.
kubectl run javawebapp --image=dockerhandson/java-web-app:1 --port=8080

# List pods from current(default) ns
kubect get pods

# List pods from given  ns
kubect get pods -n <namespaceName>

ex:
kubect get pods -n test-ns



Kubernetes Objects Examples:

POD

Replication Controller

Replica Set

DaemonSet

Deployment
Statefullset

Service

PersistentVolume

PersistentVolumeClaim

CofgigMap

Secret ..etc

# POD Manifest

apiVersion: v1
kind: Pod
metadata:
  name: <PodName>
  labels:
    <Key>: <value>
  namespace: <nameSpaceName>
spec:
  containers:
  - name: <NameOfTheCotnainer>
    image: <imagaName>
	ports:
	- containerPort: <portOfContainer>
	
Example:
---	
apiVersion: v1
kind: Pod
metadata:
  name: javawebapppod
  labels:
    app: javawebapp
  namespace: test-ns	
spec:
  containers:
  - name: javawebappcontainer
    image: dockerhandson/java-web-app:1
    ports:
    - containerPort: 8080


kubectl apply -f <fileName.yml>

kubectl apply -f <fileName.yml> -n <namespaceName>

kubectl get all 
kubectl get pods 
kubectl get pods --show-labels
kubectl get pods -o wide
kubectl get pods -o wide --show-labels

kubectl  describe pod <podName>
kubectl  describe pod <podName> -n <namespace>




# Multi Container POD
apiVersion: v1
kind: Pod
metadata:
  name:  <PODName>
  namespace: <nameSpaceName>
  labels:
    <labelKey>: <labelValue> 
spec:
  containers:
  - name: <nameOftheCotnainer>
    image: <imageName>
	ports:
	- containerPort: <portNumberOfContainer>
  - name: <nameOftheCotnainer>
    image: <imageName>
    ports:
    - containerPort: <portNumberOfContainer>
	


K8's Service   ---> In Kubernetes Service makes our pods accessable/discoverable with in the cluster or exposing them to internat.
               		service will identify pods using it's labels And Selector. Whenever we create a service a ClusterIP (virtual IP) Address will be allocated for that serivce and DNS 					entry will be created for that IP. So internally we can access using service name(DNS).
						
	
Service
========
apiVersion: v1
kind: Service
metadata:
  name: <serviceName>
  namespace: <nameSpace>
spec:
  type: <ClusterIP/NodePort>
  selector:
     <key>: <value>
  ports:
  - port: <servciePort>	# default It to 80
    targetPort: <containerPort> 
	

With in Cluster ClusterIP
==========================
apiVersion: v1
kind: Service
metadata:
  name: javawebappsvc
  namespace: test-ns  
spec:
  type: ClusterIP
  selector:
     app: javawebapp
  ports:
  - port: 80
    targetPort: 8080
    

Out side of Cluster Node Port
========================
apiVersion: v1
kind: Service
metadata:
  name: javawebappsvc
spec:
  type: NodePort
  selector:
     app: javawebapp
  ports:
  - port: 80
    targetPort: 8080
    nodePort: 30033 # This Optional if u don't mention nodePort.Kuberetes will assign.
	

kubectl apply -f <file.yml>

kubectl get svc 
kubectl get all

kubectl  describe service <serviceName>
kubectl  describe service <serviceName> -n <namespace>
kubectl  describe service <serviceName> -o wide



What is node port range?
30000-32767


kubectl get all --all-namespaces
kubectl get all -n <namespace>
kubectl get pods -n <namespace>
kubectl get pods -n <namespace> - o wide

kubectl get svc -n <namespace>

ACCESS OUTSIDE USING NODEIP:NODEPORT.


With in the cluster one application(POD) can access other applications(PODS) using Service name.

What is FQDN?
Fully Qualified Domain name. 
If one POD need access to service & which are in differnent names space we have to use FQDN of the serivce.
Syntax: <serivceName>.<namespace>.svc.cluster.local
ex: javawebappsvc.test-ns.svc.cluster.local





POD --> Pod is the smallest building block which we can deploy in k8s.Pod represents running process.Pod contains one or more containers.These container will share same network,storage and any other specifications.Pod will have unique IP Address in k8s cluster.

Pods
 SingleContainerPods --> Pod will have only one container.
 
 MultiContainerPods(SideCar) --> POD will two or more contianers.
 
We should not create pods directly for deploying applications.If pod is down it wont be rescheduled.

We have to create pods with help of controllers.Which manages POD life cycle.
	


Controllers
===========

ReplicationController
ReplicaSet
DaemonSet
Deploymnet
StatefullSet





# Replication Conrtoller
apiVersion: v1
kind: ReplicationController
metadata:
  name: <replicationControllerName>
  namespace: <nameSpaceName>
spec:
  replicas: <noOfReplicas>
  selector:
    <key>: <value>
  template: # POD Template
    metadata:
	  name: <PODName>
	  labels:
	    <key>: <value>
	spec:
	- containers:
	  - name: <nameOfTheContainer>
	    image: <imageName>
		ports:
		- containerPort: <containerPort>
  	
Example:
========
apiVersion: v1
kind: ReplicationController
metadata:
  name: javawebapprc
spec:
  replicas: 1
  selector:
    app: javawebapp
  template:
    metadata:
      name: javawebapppod
      labels:
        app: javawebapp
    spec:
      containers:
      - name: javawebappcontainer
        image: dockerhandson/java-web-app
        ports:
        - containerPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  name: javawebappservice
spec:
  type: NodePort
  selector:
     app: javawebapp
  ports:
  - port: 80
    targetPort: 8080		

# Another Appplication
apiVersion: v1
kind: ReplicationController
metadata:
  name: pythonrc
spec:
  replicas: 1
  selector:
    app: pythonapp
  template: # Pod template
    metadata:
      name: pythonapppod
      labels:
        app: pythonapp
    spec:
      containers:
      - name: pythonappcontainer
        image: dockerhandson/python-app:1
        ports:
        - containerPort: 5000
---
apiVersion: v1
kind: Service
metadata:
  name: pythonsvc
spec:
  type: NodePort
  selector:
    app: pythonapp
  ports:
  - port: 80
    targetPort: 5000
	


# Another Appplication
apiVersion: v1
kind: ReplicationController
metadata:
  namespace: test
  name: mavenwebrc
spec:
  replicas: 1
  template:
    metadata:
      name: mavenwebapppod
      labels:
        app: mavenwebapp
    spec:
      containers:
      - name: mavenwebappcontainer
        image: dockerhandson/maven-web-application:1
        ports:
        - containerPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  name: mavenwebappsvc
  namespace: test
spec:
  type: NodePort
  selector:
    app: mavenwebapp
  ports:
  - port: 80
    targetPort: 8080
    	
kubectl apply -f <filename.yml>
kubectl get rc 
kubectl get rc -n <namespace>
kubectl get all
kubectl scale rc <rcName> --replicas <noOfReplicas>

kubectl describe rc <rcName>
kubectl delete rc <rcName>    





Note: If we don't mention -n <namespace> it will refer default namespace.
If required we can change name space context.

kubctl config set-context --current --namespace=<namespace>
ex:
kubectl config set-context --current --namespace=test-ns

After setting context  by default it will point to that namespace.


Change it to default namespace again if required
ex:
kubectl config set-context --current --namespace=default





ReplicaSet:

What is difference b/w replicaset and replication controller?

It's next gernation of replication controller. Both manages the pod replicas. But only difference as now is
selector support.

RC --> Supports only equality based selectors.

key == value(Equal Condition)
selector:
    app: javawebapp

RS --> Supports eqaulity based selectors and also set based selectors.


key == value(Equal Condition)

Set Based
key in (value1,value2,value3)
key notin (value1) 

selector:
   matchLabels: # Equality Based
     key: value
   matchExpressions: # Set Based
   - key: app
     operator: IN
	 values:
	 - javawebpp
	 - javawebapplication
	 
# Mainfest File RS

apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: <RSName>
spec:
  replicas: <noOfPODReplicas>
  selector:  # To Match POD Labels.
    matchLabels:  # Equality Based Selector
	  <key>: <value>
    matchExpressions:  # Set Based Selector 
	- key: <key>
	  operator: <in/not in>
	  values:
	  - <value1>
	  - <value2>
  template:
    metadata:
	  name: <PODName>
	  labels:
	    <key>: <value>
	spec:
	- containers:
	  - name: <nameOfTheContainer>
	    image: <imageName>
		ports:
		- containerPort: <containerPort>


Example:

apiVersion: apps/v1
kind: ReplicaSet
metadata: 
  name: javawebapprs
spec: 
  replicas: 1
  selector: 
    matchLabels: 
      app: javawebapp
  template: 
    metadata: 
	  name: javawebapppod
      labels: 
        app: javawebapp
    spec: 
      containers: 
      - image: dockerhandson/java-web-app:1
        name: javawebappcontainer
        ports: 
        - containerPort: 8080


kubectl get rs 
kubectl get rs -n <namespace>
kubectl get all
kubectl scale rs <rsName> --replicas <noOfReplicas>

kubectl describe rs <rsName>
kubectl delete rs <rsName>






What is difference b/w kubectl create and kubectl apply ?

Create will Create an Object if it's not already created. Apply will perfrom create if object is not created earlier.If it's already
created it will update.			   
			   
			   
			   	

kubectl apply (create & update)

kubectl create -f <fileName.yml>

kubectl update -f <fileName.yml>


Change/Switch Context(NameSpace)
=================================

# View kubectl context
kubectl config view | grep namespace


# Change/Switch namespace

kubectl config set-context --current  --namespace=<namespace>




apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: <RSName>
spec:
  selector:  # To Match POD Labels.
    matchLabels:  # Equality Based Selector
	  <key>: <value>
    matchExpressions:  # Set Based Selector 
	- key: <key>
	  operator: <in/not in>
	  values:
	  - <value1>
	  - <value2>
  template:
    metadata:
	  name: <PODName>
	  labels:
	    <key>: <value>
	spec:
	- containers:
	  - name: <nameOfTheContainer>
	    image: <imageName>
		ports:
		- containerPort: <containerPort>


apiVersion: apps/v1
kind: DaemonSet
metadata: 
  name: mavenwebappds
spec: 
  selector: 
    matchLabels: 
      app: mavenwebapp
  template: 
    metadata: 
	  name: mavenwebapppod
      labels: 
        app: mavenwebapp
    spec: 
      containers: 
      - image: dockerhandson/maven-web-app
        name: mavenwebappcontainer
        ports: 
        - containerPort: 8080
		
kubectl get ds 
kubectl get ds -n <namespace>
kubectl get all


kubectl describe ds <dsName>
kubectl delete ds <dsName>



# Deployment ReCreate
apiVersion: apps/v1
kind: Deployment
metadata:
  name: javawebappdeployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: javawebapp
  strategy:
    type: Recreate    
  template:
    metadata:
      name: javawebapppod
      labels:
        app: javawebapp
    spec:
      containers:
      - name: javawebappcontainer
        image: dockerhandson/java-web-app:1
        ports:
        - containerPort: 8080

kubectl get deployment
kubectl get rs
kubectl get pods
kubectl rollout status deployment <deploymentName>
kubectl rollout history  deployment <deploymentName>
kubectl rollout history  deployment <deploymentName> --revision 1  
kubectl scale deployment <deploymentName> --replicas <noOfReplicas>

We can update deployment using yml or using command
	
	
# Update Deployment Image using command	

kubectl set image deployment <deploymentName> <containerName>=<imageNameWithVersion> --record		
ex:	
kubectl set image deployment javawebappdeployment javawebappcontainer=dockerhandson/java-web-app:2 --record		

Roll back to previous revison
kubectl rollout undo  deployment <deploymentName> --to-revision 1



# Rolling Update
apiVersion: apps/v1
kind: Deployment
metadata:
  name: javawebappdeployment
spec:
  replicas: 2
  revisionHistoryLimit: 5
  selector:
    matchLabels:
      app: javawebapp
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 1
      maxSurge: 1
  minReadySeconds: 30
  template:
    metadata:
      name: javawebapppod
      labels:
        app: javawebapp
    spec:
      containers:
      - name: javawebappcontainer
        image: dockerhandson/java-web-app:1
        ports:
        - containerPort: 8080 


kubectl get deployment
kubectl get rs
kubectl get pods
kubectl rollout status deployment <deploymentName>
kubectl rollout history  deployment <deploymentName>
kubectl rollout history  deployment <deploymentName> --revision 1  
kubectl rollout undo  deployment <deploymentName> --to-revision 1  
kubectl scale deployment <deploymentName> --replicas <noOfReplicas>
	
# Update Deployment Image using command	

kubectl set image deployment <deploymentName> <containerName>=<imageNameWithVersion> --record
    


	


POD AutoScaler
==============
What is difference b/w Kubernetes AutoScaling(POD AutoScaling) & AWS AutoScaling?


POD AutoScaling --> Kuberenets POD AutoScaling Will make sure u have minimum number pod replicas available at any time & based the observed CPU/Memory utilization on pods it can scale PODS.  HPA Will Scale up/down pod replicas of Deployment/ReplicaSet/ReplicationController based on observerd CPU & Memory utilization base the target specified.


AWS AutoScaling --> It will make sure u have enough number of nodes(Servers). Always it will maintian minimum number of nodes. Based the observed CPU/Memory utilization of node it can scale nodes.


Note: Deploy metrics server as k8s addon which will fetch metrics. Follow bellow link to deploy metrics Server.
====
https://github.com/MithunTechnologiesDevOps/metrics-server





---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hpadeployment
spec:
  replicas: 2
  selector:
    matchLabels:
      name: hpapod
  template:
    metadata:
      labels:
        name: hpapod
    spec:
      containers:
        - name: hpacontainer
          image: k8s.gcr.io/hpa-example
          ports:
          - name: http
            containerPort: 80
          resources:
            requests:
              cpu: "100m"
              memory: "64Mi"
            limits:
              cpu: "100m"
              memory: "256Mi"
---
apiVersion: v1
kind: Service
metadata:
  name: hpaclusterservice
  labels:
    name: hpaservice
spec:
  ports:
    - port: 80
      targetPort: 80
  selector:
    name: hpapod
  type: NodePort
---
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: hpadeploymentautoscaler
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: hpadeployment
  minReplicas: 2
  maxReplicas: 5
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 40
  - type: Resource
    resource:
     name: memory
     target:
      type: Utilization
      averageUtilization: 40
	  

# Create temp POD using below command interatively and increase the load on demo app by accessing the service.

kubectl run -i --tty load-generator --rm  --image=busybox /bin/sh


# Access the service to increase the load.

while true; do wget -q -O- http://hpaclusterservice; done





# Java Web Appliction With HPA
apiVersion: apps/v1
kind: Deployment
metadata:
  name: javawebappdeployment
  namespace: test-ns
spec:
  selector:
    matchLabels:
      app: javawebapp
  strategy:
    type: Recreate
  template:
    metadata:
      name: javawebapppod
      labels:
        app: javawebapp
    spec:
      containers:
      - name: javawebappcontainer
        image: dockerhandson/java-web-app:4
        ports:
        - containerPort: 8080
        resources:
          requests:
            cpu: 100m
            memory: 256Mi
          limits:
            cpu: 200m
            memory: 512Mi
---

apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: javawebappdeploymenthpa
  namespace: test-ns
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: javawebappdeployment
  minReplicas: 2
  maxReplicas: 5
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 90
  - type: Resource
    resource:
     name: memory
     target:
      type: Utilization
      averageUtilization: 90
---
apiVersion: v1
kind: Service
metadata:
  name: javawebappsvc
  namespace: test-ns
spec:
  type: NodePort
  selector:
    app: javawebapp
  ports:
  - port: 80
    targetPort: 8080
	




# Spring App & Mongod DB as POD with out volumes

apiVersion: apps/v1
kind: Deployment
metadata:
  name: springappdeployment
spec:
  selector:
    matchLabels:
      app: springapp
  template:
    metadata:
      labels:
        app: springapp
    spec:
      containers:
      - name: springappcontainer
        image: dockerhandson/spring-boot-mongo:1
        resources:
          requests:
            cpu: 200m
            memory: 256Mi
          limits:
            memory: "512Mi"
            cpu: "500m"
        ports:
        - containerPort: 8080
        env:
        - name: MONGO_DB_HOSTNAME
          value: mongosvc
        - name: MONGO_DB_USERNAME
          value: devdb
        - name: MONGO_DB_PASSWORD
          value: devdb@123
---
apiVersion: v1
kind: Service
metadata:
  name: springappsvc
spec:
  type: NodePort
  selector:
    app: springapp
  ports:
  - port: 80
    targetPort: 8080
---
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: mongo
spec:
  selector:
    matchLabels:
      app: mongo
  template:
    metadata:
      name: mongo
      labels:
        app: mongo
    spec:
      containers:
        - name: mognodbcontainer
          image: mongo
          ports:
          - containerPort: 27017
          env:
          - name: MONGO_INITDB_ROOT_USERNAME
            value: devdb
          - name: MONGO_INITDB_ROOT_PASSWORD
            value: devdb@123
---
apiVersion: v1
kind: Service
metadata:
  name: mongosvc
spec:
  type: ClusterIP
  selector:
    app: mongo
  ports:
  - port: 27017
    targetPort: 27017



Volumes:

Kubernetes Supports different types of volumes.

hostPath
nfs
emptydir
configMap
Secret

awsElasticBlockStore
googlePersistantdisk
azureFile
azuredisk

persistantVolume
persistantVolumeClaim



## Mongo db POD with Host Path Volume##

## Spring Boot App  
apiVersion: apps/v1
kind: Deployment
metadata:
  name: springappdeployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: springapp
  template:
    metadata:
      name: springapppod
      labels:
        app: springapp
    spec:
      containers:
      - name: springappcontainer
        image: dockerhandson/spring-boot-mongo
        ports:
        - containerPort: 8080
        env:
        - name: MONGO_DB_USERNAME
          value: devdb
        - name: MONGO_DB_PASSWORD
          value: devdb@123
        - name: MONGO_DB_HOSTNAME
          value: mongo 
---
apiVersion: v1
kind: Service
metadata:
  name: springapp
spec:
  selector:
    app: springapp
  ports:
  - port: 80
    targetPort: 8080
  type: NodePort
---
# Mongo db pod with volumes(HostPath)
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongodbdeployment
spec:
  selector:
    matchLabels:
      app: mongodb
  template:
     metadata:
       name: mongodbpod
       labels:
         app: mongodb
     spec:
       volumes:
       - name: hostpathvol
         hostPath:
           path: /tmp/mongodb 
       containers:
       - name: mongodbcontainer
         image: mongo
         ports:
         - containerPort: 27017
         env:
         - name: MONGO_INITDB_ROOT_USERNAME
           value: devdb
         - name: MONGO_INITDB_ROOT_PASSWORD
           value: devdb@123
         volumeMounts:
         - name: hostpathvol
           mountPath: /data/db   
---
apiVersion: v1
kind: Service
metadata:
  name: mongo
spec:
  type: ClusterIP
  selector:
    app: mongodb
  ports:
  - port: 27017
    targetPort: 27017
	

	

Configuration of NFS Server
===========================

Step 1: 

Create one Server for NFS

Install NFS Kernel Server in 
Before installing the NFS Kernel server, we need to update our system’s repository index with that of the Internet through the following apt command as sudo:

$ sudo apt-get update

The above command lets us install the latest available version of a software through the Ubuntu repositories.

Now, run the following command in order to install the NFS Kernel Server on your system:

$ sudo apt install nfs-kernel-server


Step 2: Create the Export Directory

sudo mkdir -p /mnt/nfs_share/

# As we want all clients to access the directory, we will remove restrictive permissions.
sudo chown nobody:nogroup /mnt/nfs_share/
sudo chmod 777 /mnt/nfs_share/

Step 3: Assign server access to client(s) through NFS export file

sudo vi /etc/exports


#/mnt/share/ <clientIP or Clients CIDR>(rw,sync,no_subtree_check,no_root_squash)
 #Ex:
/mnt/nfs_share/ *(rw,sync,no_subtree_check,no_root_squash)




Step 4: Export the shared directory

$ sudo exportfs -a



sudo systemctl restart nfs-kernel-server

Step 5: Open firewall for the client (s) PORT 2049




Configuring the Client Machines(Kubernetes Nodes)
================================================

Step 1: Install NFS Common
Before installing the NFS Common application, we need to update our system’s repository index with that of the Internet through the following apt command as sudo:

$ sudo apt-get update


$ sudo apt-get install nfs-common


Deploy mongdb pods using NFS Volume in k8s


#Mongo db POD with NFS Volume ##
apiVersion: apps/v1
kind: Deployment
metadata:
  name: springappdeployment
spec:
 replicas: 2
 selector:
   matchLabels:
     app: springapp
 template:
   metadata:
     name: springapppod
     labels:
       app: springapp
   spec:
      containers:
      - name: springappcontainer
        image: dockerhandson/spring-boot-mongo
        ports:
        - containerPort: 8080
        env:
        - name: MONGO_DB_HOSTNAME
          value: mongo
        - name: MONGO_DB_USERNAME
          value: devdb
        - name: MONGO_DB_PASSWORD
          value: devdb@123
---
apiVersion: v1
kind: Service
metadata:
  name: springappsvc
spec:
  type: NodePort
  selector:
    app: springapp
  ports:
  - port: 80
    targetPort: 8080
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mognodbrs
spec:
  selector:
    matchLabels:
      app: mongo
  template:
    metadata:
      name: mongodbpod
      labels:
        app: mongo
    spec:
      containers:
      - name: mongodbcontainer
        image: mongo
        ports:
        - containerPort: 27017
        env:
        - name: MONGO_INITDB_ROOT_USERNAME
          value: devdb
        - name: MONGO_INITDB_ROOT_PASSWORD
          value: devdb@123
        volumeMounts:
        - name: mongodnfsvol
          mountPath: /data/db
      volumes:
      - name: mongodnfsvol
        nfs:
          server: 172.31.38.98  # Update NFS Server IP And Path Based on your setup
          path: /mnt/nfs_share
---
apiVersion: v1
kind: Service
metadata:
  name: mongo
spec:
  type: ClusterIP
  selector:
    app: mongo
  ports:
  - port: 27017
    targetPort: 27017
    




PV --> It's a piece of storage(hostPath,nfs,ebs,azurefile,azuredisk) in k8s cluster. PV exists independently from 
from pod life cycle whihc is consuming.

Persistent Volumes are provisioned in two ways, Statically or Dynamically.

1) Static Volumes (Manual Provisionging)
    As a k8's Administrator will create a PV manullay so that pv's can be avilable for PODS which requires.
	Create a PVC so that PVC will be attached PV. We can use PVC with PODS to get an access to PV. 
	
2) Dynamic Volumes (Dynamic Provisioning)
     It's possible to have k8's provsion(Create) volumes(PV) as required. Provided we have configured storageClass.
	 So when we create PVC if PV is not available Storage Class will Create PV dynamically.
   

PVC
If pod requires access to storage(PV),it will get an access using PVC. PVC will be attached to PV.



PersistentVolume – the low level representation of a storage volume.
PersistentVolumeClaim – the binding between a Pod and PersistentVolume.
Pod – a running container that will consume a PersistentVolume.
StorageClass – allows for dynamic provisioning of PersistentVolumes.


PV Will have Access Modes

ReadWriteOnce – the volume can be mounted as read-write by a single node
ReadOnlyMany – the volume can be mounted read-only by many nodes
ReadWriteMany – the volume can be mounted as read-write by many nodes

In the CLI, the access modes are abbreviated to:

RWO - ReadWriteOnce
ROX - ReadOnlyMany
RWX - ReadWriteMany


Claim Policies

A Persistent Volume Claim can have several different claim policies associated with it including

Retain – When the claim(PVC) is deleted, the volume(PV) will exists.
Recycle – When the claim is deleted the volume remains but in a state where the data can be manually recovered.
Delete – The persistent volume is deleted when the claim is deleted.
The claim policy (associated at the PV and not the PVC) is responsible for what happens to the data on when the claim has been deleted.


Commands

kubectl get pv
kubectl get pvc
kubectl get storageclass
kubectl describe pvc <pvcName>
kubectl describe pv <pvName>



If Storage is calss not configued
=================================
1) Create a PV manually if not already available

2) Claim the PV by creating PVC

3) Use that PVC in your pod manfiset


If Storage is calss configued
=============================

1) Claim the PV by creating PVC

2) Use that PVC in your pod manfiset




Find Sample PV & PVC Yml from below Git Hub

https://github.com/MithunTechnologiesDevOps/Kubernates-Manifests/tree/master/pv-pvc

Static Volumes
1) Create PV

apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-hostpath
spec:
  capacity:
    storage: 1Gi
  accessModes:
  - ReadWriteOnce
  hostPath:
    path: "/mongodata"

2) Create PVC

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mongopvc
spec:
  storageClassName: manual
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
		   
3) Use PVC with POD in POD manifest.

# Mongo db pod with PVC
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: mongodbrs
spec:
  selector:
    matchLabels:
      app: mongodb
  template:
     metadata:
       name: mongodbpod
       labels:
         app: mongodb
     spec:
       volumes:
       - name: mongovol
         persistentVolumeClaim:
           claimName: mongopvc
       containers:
       - name: mongodbcontainer
         image: mongo
         ports:
         - containerPort: 27017
         env:
         - name: MONGO_INITDB_ROOT_USERNAME
           value: devdb
         - name: MONGO_INITDB_ROOT_PASSWORD
           value: devdb@123
         volumeMounts:
         - name: mongovol
           mountPath: /data/db



Commands://
=========

kubectl get pv
kubectl get pvc

kubectl describe pv <pvName>
kubectl describe pvc <pvcName>        






kubectl get storageclass

Note: Configure Storage Class for Dynamic Volumes based on infra sturcture. Make that one as default storage class.

NFS Provisioner
Prerequisiets:
1) NFS Server
2) Insall nfs client softwares in all k'8s nodes.

Find NFS Provisioner below.

https://raw.githubusercontent.com/MithunTechnologiesDevOps/Kubernates-Manifests/master/pv-pvc/nfsstorageclass.yml

Get yml from above link.

$ curl https://raw.githubusercontent.com/MithunTechnologiesDevOps/Kubernates-Manifests/master/pv-pvc/nfsstorageclass.yml >> nfsstorageclass.yml

And update Your NFS Server IP Address(2 Places you need update IP Addrees) And path of nfs share. Apply

kubectl apply -f nfsstorageclass.yml

Dynamic Volumes

Refer below link where we are creating PVC & PODS :

https://raw.githubusercontent.com/MithunTechnologiesDevOps/Kubernates-Manifests/master/SpringBoot-Mongo-DynamicPV.yml

1) Create PVC(If we don't mention storageclass name it will use defautl storage class which is configured.) It will create PV.

apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mongodb-nfs-pvc
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 1Gi
	  
2) Use PVC with POD in POD manifest.

apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: mongodbrs
spec:
  selector:
    matchLabels:
      app: mongodb
  template:
     metadata:
       name: mongodbpod
       labels:
         app: mongodb
     spec:
       volumes:
       - name: mongodb-pvc
         persistentVolumeClaim:
           claimName: mongodb-nfs-pvc   
       containers:
       - name: mongodbcontainer
         image: mongo
         ports:
         - containerPort: 27017
         env:
         - name: MONGO_INITDB_ROOT_USERNAME
           value: devdb
         - name: MONGO_INITDB_ROOT_PASSWORD
           value: devdb@123
         volumeMounts:
         - name: mongodb-pvc
           mountPath: /data/db
		   
# Complete Manifest Where in single yml we defined Deployment & Service for SpringApp & PVC(with NFS Dynamic StorageClass),ReplicaSet & Service For Mongo.

apiVersion: apps/v1
kind: Deployment
metadata:
  name: springappdeployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: springapp
  template:
    metadata:
      name: springapppod
      labels:
        app: springapp
    spec:
      containers:
      - name: springappcontainer
        image: dockerhandson/spring-boot-mongo
        ports:
        - containerPort: 8080
        env:
        - name: MONGO_DB_USERNAME
          value: devdb
        - name: MONGO_DB_PASSWORD
          value: devdb@123
        - name: MONGO_DB_HOSTNAME
          value: mongo 
---
apiVersion: v1
kind: Service
metadata:
  name: springapp
spec:
  selector:
    app: springapp
  ports:
  - port: 80
    targetPort: 8080
    nodePort: 30032
  type: NodePort
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mongodbpvc 
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 100Mi
---
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: mongodbrs
spec:
  selector:
    matchLabels:
      app: mongodb
  template:
     metadata:
       name: mongodbpod
       labels:
         app: mongodb
     spec:
       volumes:
       - name: pvc
         persistentVolumeClaim:
           claimName: mongodbpvc     
       containers:
       - name: mongodbcontainer
         image: mongo
         ports:
         - containerPort: 27017
         env:
         - name: MONGO_INITDB_ROOT_USERNAME
           value: devdb
         - name: MONGO_INITDB_ROOT_PASSWORD
           value: devdb@123
         volumeMounts:
         - name: pvc
           mountPath: /data/db   
---
apiVersion: v1
kind: Service
metadata:
  name: mongo
spec:
  type: ClusterIP
  selector:
    app: mongodb
  ports:
  - port: 27017
    targetPort: 27017
	




Config Maps & Secrets
======================

We can create ConfigMap & Secretes in Cluster using command or also using yml.


ConfigMap Using Command
======================
kubectl create configmap springappconfig --from-literal=mongodbusername=devdb


Or Using yml

---
apiVersion: v1
kind: ConfigMap
metadata:      # We can define multiple key value pairs.
  name: springappconfig
data:
  mongodbusername: devdb
  
  
Secret Using Command: 

kubectl create secret generic springappsecret --from-literal=mongodbpassword=devdb@123


Using Yml:

apiVersion: v1
kind: Secret
metadata:
  name: springappsecret
type: Opaque
stringData:   # We can define multiple key value pairs.
  mongodbpassword: devdb@123    
  

In Production Cluster we can create with differnet values.

kubectl create configmap springappconfig --from-literal=mongodbusername=proddb 

apiVersion: v1
kind: ConfigMap
metadata:
  name: springappconfig
data:            # We can define multiple key value pairs.
  mongodbusername: proddb

kubectl create secret generic springappsecret --from-literal=mongodbpassword=proddb@123


Using Yml:

apiVersion: v1
kind: Secret
metadata:
  name: springappsecret
type: Opaque
stringData:   # We can define multiple key value pairs.
  mongodbpassword: prodb@123
  

apiVersion: apps/v1
kind: Deployment
metadata:
  name: springappdeployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: springapp
  template:
    metadata:
      labels:
        app: springapp
    spec:
      containers:
      - name: springappcontainer
        image: dockerhandson/spring-boot-mongo:1
        env:
        - name: MONGO_DB_HOSTNAME
          value: mongosvc
        - name: MONGO_DB_USERNAME
          valueFrom:
            configMapKeyRef:
              name: springappconfig
              key: mongodbusername
        - name: MONGO_DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: springappsecret
              key: mongodbpassword
        resources:
          limits:
            memory: "512Mi"
            cpu: "500m"
          requests:
            cpu: "200m"
            memory: "256Mi"
        ports:
        - containerPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  name: springappsvc
spec:
  type: NodePort
  selector:
    app: springapp
  ports:
  - port: 80
    targetPort: 8080
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongodeployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mongo
  template:
    metadata:
      labels:
        app: mongo
    spec:
      containers:
      - name: mongocontainer
        image: mongo
        ports:
        - containerPort: 27017
        env:
        - name: MONGO_INITDB_ROOT_USERNAME
          valueFrom:
            configMapKeyRef:
              name: springappconfig
              key: mongodbusername
        - name: MONGO_INITDB_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: springappsecret
              key:  mongodbpassword
        volumeMounts:
        - name: mongodbhostvol
          mountPath: /data/db
      volumes:
      - name: mongodbhostvol
        hostPath:
          path: /tmp/mongo
---
apiVersion: v1
kind: Service
metadata:
  name: mongosvc
spec:
  selector:
    app: mongo
  ports:
  - port: 27017
    targetPort: 27017
    




ConigMap As Volume Example
=========================

# ConfigMap with file data

apiVersion: v1
kind: ConfigMap
metadata:
  name: javawebappconfig
data:
  tomcat-users.xml: |
    <?xml version='1.0' encoding='utf-8'?>
      <tomcat-users xmlns="http://tomcat.apache.org/xml"
                      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
                      xsi:schemaLocation="http://tomcat.apache.org/xml tomcat-users.xsd"
                      version="1.0">
       <user username="tomcat" password="tomcat" roles="admin-gui,manager-gui"/>
    </tomcat-users>
	
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: javawebdeployment
spec:
  replicas: 2
  strategy:
    type: Recreate
  selector:
    matchLabels:
      app: javawebapp
  template:
    metadata:
      name: javawebappod
      labels:
        app: javawebapp
    spec:
      containers:
      - name: javawebappcontainer
        image: dockerhandson/java-web-app:3
        ports:
        - containerPort: 8080
        volumeMounts:
        - name: tomcatusersconfig
          mountPath: "/usr/local/tomcat/conf/tomcat-users.xml"
          subPath: "tomcat-users.xml"
      volumes:
      - name: tomcatusersconfig
        configMap:
          name: javawebappconfig
          items:
          - key: "tomcat-users.xml"
            path: "tomcat-users.xml"



			
Pull an Image from a Private Registry
=====================================

kubectl create secret docker-registry regcred --docker-server=<your-registry-server> --docker-username=<your-name> --docker-password=<your-pword> --docker-email=<your-email>


<your-registry-server> is your Private Docker Registry FQDN. Use https://index.docker.io/v1/ for DockerHub.
<your-name> is your Docker username.
<your-pword> is your Docker password.
<your-email> is your Docker email.

ex: 
Docker Hub: --docker-server is optional in case of docker hub

kubectl create secret docker-registry regcred --docker-server=https://index.docker.io/v1/ --docker-username=dockerhandson --docker-password=password

ECR # Get ECR password using AWS CLI and use the password below. If its EKS cluster we just need to attache ECR Policies(Permsisssions) to IAM Role and attach that role EKS nodes.No
need to create a secret and use that as imagepull secret.

kubectl create secret docker-registry ecrregistrycredentails --docker-server=https://567763916643.dkr.ecr.ap-south-1.amazonaws.com --docker-username=AWS --docker-password=password
				
# Nexus
kubectl create secret docker-registry nexuscred --docker-server=172.31.106.247:8083 --docker-username=admin --docker-password=admin123


Use above scret as imagepull screts in pod template.	 






Liveness Probe & Ready ness Probes
==================================  				

apiVersion: apps/v1
kind: Deployment
metadata:
  name: javawebappdeployment
spec:
  replicas: 2
  revisionHistoryLimit: 10
  strategy:
    type: Recreate
  selector:
    matchLabels:
      app: javawebapp
  template:
    metadata:
      name: javawebapppod
      labels:
        app: javawebapp
    spec:
      containers:
      - name: javawebappcontainer
        image: dockerhandson/java-web-app:1
        ports:
        - containerPort: 8080
        resources:
          requests:
            cpu: 200m
            memory: 256Mi
          limits:
            cpu: 1
            memory: 1Gi
        livenessProbe:
          httpGet:
            path: /java-web-app
            port: 8080
          initialDelaySeconds: 60
          periodSeconds: 30
	  timeoutSeconds: 5
        readinessProbe:
          httpGet:
            path: /java-web-app
            port: 8080
          initialDelaySeconds: 60
          periodSeconds: 10
          timeoutSeconds: 5
---
apiVersion: v1
kind: Service
metadata:
 name: javawebappsvc
spec:
  type: NodePort
  selector:
    app: javawebapp
  ports:
  - port: 80
    targetPort: 8080
    




####################################
# Mongo Database as statefullSet
####################################

apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: mongod
  namespace: test
spec:
  #terminationGracePeriodSeconds: 10
  selector:
    matchLabels:
      app: mongod
  serviceName: mongodb-service
  replicas: 3
  template:
    metadata:
      labels:
        app: mongod
    spec:
      terminationGracePeriodSeconds: 10
      containers:
      - name: mongodbcontainer
        image: mongo
        command:
         - "mongod"
         - "--bind_ip"
         - "0.0.0.0"
         - "--replSet"
         - "MainRepSet"
        resources:
          requests:
            cpu: 200m
            memory: 128Mi
          limits:
            cpu: 200m
            memory: 256Mi
        ports:
        - containerPort: 27017
        volumeMounts:
        - name: mongodb-persistent-storage-claim
          mountPath: "/data/db"
  volumeClaimTemplates:
  - metadata:
      name: mongodb-persistent-storage-claim
    spec:
      accessModes: [ "ReadWriteOnce" ]
      resources:
        requests:
          storage: 1Gi
---
apiVersion: v1
kind: Service
metadata:
  name: mongodb-service
  namespace: test
spec:
  clusterIP: None # Headless Service
  selector:
    app: mongod
  ports:
  - port: 27017
    targetPort: 27017

# Setup Mongodb Reple Set And Added Members And Create the Administrator for the MongoDB

# Go inside one of the pod

kubectl exec -it mongod-0  bash

# Connect to mongo shell by using below command

mongo

# Initiate mongod db reple set and add members

rs.initiate( { _id: "MainRepSet", version: 1,
members: [ 
 { _id: 0, host: "mongod-0.mongodb-service.test.svc.cluster.local:27017" }, 
 { _id: 1, host: "mongod-1.mongodb-service.test.svc.cluster.local:27017" }, 
 { _id: 2, host: "mongod-2.mongodb-service.test.svc.cluster.local:27017" } ] } );
 
# Create root user name and password 
db.getSiblingDB("admin").createUser( {user : "devdb",pwd  : "devdb123",roles: [ { role: "root", db: "admin" } ] } ); 	


# Spring App ConfigMap & Secret And use(refer) these in your pod manifest or directly define as env values.

apiVersion: v1
kind: ConfigMap
metadata:
  name: springappconfig
data:
  mongodbusername: devdb
---
apiVersion: v1
kind: Secret
metadata:
  name: springappsecret
type: Opaque
stringData:
  mongodbpassword: devdb123
  

# Deploy Spring App which connects to mongodb


apiVersion: apps/v1
kind: Deployment
metadata:
  name: springappdeployment
  namespace: test
spec:
  replicas: 2
  selector:
    matchLabels:
      app: springapp
  template:
    metadata:
      name: springapppod
      labels:
        app: springapp
    spec:
      containers:
      - name: springappcontainer
        image: dockerhandson/spring-boot-mongo:1
        ports:
        - containerPort: 8080
        resources:
          requests:
            cpu: 200m
            memory: 256Mi
          limits:
            cpu: 300m
            memory: 256Mi
        env:
        - name: MONGO_DB_USERNAME
          value: devdb
        - name: MONGO_DB_PASSWORD
          value: devdb123
        - name: MONGO_DB_HOSTNAME
          value: mongodb-service
---
apiVersion: v1
kind: Service
metadata:
  name: springapp
  namespace: test
spec:
  selector:
    app: springapp
  ports:
  - port: 80
    targetPort: 8080
  type: NodePort

Commands
========
kubectl get pv
kubectl get pvc
kubectl get statefulset

kubectl delete statefulset <statefulsetName>	






Node Selector  Node Affinity And Taints,Tolerations
===================================================

kubectl get nodes

kubectl get nodes --show-labels

kubectl describe node <nodeId>

# Add Label to Node
kubectl label nodes <nodeId/Name> node=workerOne


# Node Selector
apiVersion: apps/v1
kind: Deployment
metadata:
  name: javawebapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: javawebapp
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
  minReadySeconds: 60
  template:
    metadata:
      name: javawebapp
      labels:
        app: javawebapp
    spec:
      nodeSelector:
        name: workerOne
      containers:
      - name: javawebapp
        image: dockerhandson/java-web-app:3
        ports:
        - containerPort: 8080

---		
# requiredDuringSchedulingIgnoredDuringExecution(HardRule)
apiVersion: apps/v1
kind: Deployment
metadata:
  name: javawebapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: javawebapp
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
  minReadySeconds: 60
  template:
    metadata:
      name: javawebapp
      labels:
        app: javawebapp
    spec:
      affinity:
        nodeAffinity:
         requiredDuringSchedulingIgnoredDuringExecution:
           nodeSelectorTerms:
           - matchExpressions:
             - key: "node"
               operator: In
               values:
               - workerOne
      containers:
      - name: javawebapp
        image: dockerhandson/java-web-app:3
        ports:
        - containerPort: 8080
---		
# preferredDuringSchedulingIgnoredDuringExecution(Soft Rule)   
apiVersion: apps/v1
kind: Deployment
metadata:
  name: javawebapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: javawebapp
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
  minReadySeconds: 60
  template:
    metadata:
      name: javawebapp
      labels:
        app: javawebapp
    spec:
      affinity:
        nodeAffinity:
         preferredDuringSchedulingIgnoredDuringExecution:
         - weight: 1
           preference:
            matchExpressions:
            - key: name
              operator: In
              values:
              - workerone
      containers:
      - name: javawebapp
        image: dockerhandson/java-web-app:3
        ports:
        - containerPort: 8080
		
Pod Affinity
------------

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginxdeployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      name: nginxpod
      labels:
        app: nginx
    spec:
      containers:
      - name: nginxcontainer
        image: nginx
        ports:
        - containerPort: 80
---		
apiVersion: apps/v1
kind: Deployment
metadata:
  name: javawebappdeployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: javawebapp
  strategy:
    type: Recreate
  template:
    metadata:
      name: javawebappod
      labels:
        app: javawebapp
    spec:
      affinity:
        podAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
          - labelSelector:
              matchExpressions:
              - key: app
                operator: In
                values:
                - nginx
            topologyKey: "kubernetes.io/hostname"
      containers:
      - name: javawebappcontainer
        image: dockerhandson/java-web-app:4
        ports:
        - containerPort: 8080

Pod AntiAffinity
----------------

apiVersion: apps/v1
kind: Deployment
metadata:
  name: javawebappdeployment
spec:
  replicas: 2
  strategy:
    type: Recreate
  selector:
    matchLabels:
      app: javawebapp
  template:
    metadata:
      name: javawebapppod
      labels:
        app: javawebapp
    spec:
      affinity:
        podAntiAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
          - labelSelector:
              matchExpressions:
              - key: app
                operator: In
                values:
                - nginx
            topologyKey: "kubernetes.io/hostname"
      containers:
      - name: javawebapp
        image: dockerhandson/java-web-app:3
        ports:
        - containerPort: 8080
        resources:
          requests:
            cpu: 100m
            memory: 128Mi
          limits:
            cpu: 1
            memory: 1Gi
---
apiVersion: v1
kind: Service
metadata:
  name: javawebappsvc
spec:
  type: NodePort
  selector:
    app: javawebapp
  ports:
  - port: 80
    targetPort: 8080
	




# Taint a node
kubectl taint nodes <nodeId/Name> <key>=<value>:<effect>

Example:
=======
kubectl taint nodes ip-172-31-34-69 node=HatesPods:NoSchedule

# Tolerating above taint.		
apiVersion: apps/v1
kind: Deployment
metadata:
  name: javawebapp
spec:
  replicas: 1
  selector:
    matchLabels:
      app: javawebapp
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
  minReadySeconds: 60
  template:
    metadata:
      name: javawebapp
      labels:
        app: javawebapp
    spec:
      tolerations:
      - effect: NoSchedule
		operator: "Exists"
        key: node
      containers:
      - name: javawebapp
        image: dockerhandson/java-web-app:3
        ports:
        - containerPort: 8080		






Resource Quotas:
===============

When several users or teams share a cluster with a fixed number of nodes, there is a concern that one team could use more than its fair share of resources.

Resource quotas are a tool for administrators to address this concern.

A resource quota, defined by a ResourceQuota object, provides constraints that limit aggregate resource consumption per namespace. It can limit the quantity of objects that can be created in a namespace by type, as well as the total amount of compute resources(CPU,Memory) that may be consumed by resources in that namespace.

Resource quotas work like this:

1) The administrator creates one ResourceQuota for each namespace.

2) Users create resources (pods, services, etc.) in the namespace, and the quota system tracks usage to ensure it does not exceed hard resource limits defined in a ResourceQuota.

3) If creating or updating a resource violates a quota constraint, the request will fail with HTTP status code 403 FORBIDDEN with a message explaining the constraint that would have been violated.

4) If quota is enabled in a namespace for compute resources like cpu and memory, users must specify requests or limits for those values; otherwise, the quota system may reject pod creation. 

Hint: Use the LimitRange admission controller to force defaults for pods that make no compute resource requirements.



apiVersion: v1
kind: Namespace
metadata:
  name: testns
---
#Resource Quota
apiVersion: v1
kind: ResourceQuota
metadata:
  name: testns-qs-quota
  namespace: test
spec:
  hard:
    requests.cpu: "0.5"
    requests.memory: 1Gi
    limits.cpu: "1"
    limits.memory: 2Gi
    pods: 3	
	
---
# LimitRange
apiVersion: v1
kind: LimitRange
metadata:
  name: testns-limit-range
  namespace: test
spec:
  limits:
  - default:
      cpu: 200m
      memory: 512Mi
    defaultRequest:
      cpu: 100m
      memory: 256Mi
    type: Container    
    
    


Change/Switch Context(NameSpace or Cluster)
=================================

# View kubectl context
kubectl config view | grep namespace


# Change/Switch Context(Cluster)

kubectl config set-context <ConextName/ClusterName> 

# Change/Switch namespace

kubectl config set-context --current  --namespace=<namespace>

ex:


kubectl config set-context --current  --namespace=test

kubectl config set-context --current  --namespace=default


	
Network policies
=================

Network policies are Kubernetes resources that control the traffic between pods and/or network endpoints. They uses labels to select pods and specify the traffic that is directed toward those pods using rules. Most CNI plugins support the implementation of network policies, however, if they don’t and we create a NetworkPolicy, then that resource will be ignored.

The most popular CNI plugins with network policy support are:
Weave
Calico
Cilium
Romana					
		

In Kubernetes, pods are capable of communicating with each other and will accept traffic from any source, by default. With NetworkPolicy we can add traffic restrictions to any number of selected pods, while other pods in the namespace (those that go unselected) will continue to accept traffic from anywhere. The NetworkPolicy resource has mandatory fields such as apiVersion, kind, metadata and spec. Its spec field contains all those settings which define network restrictions within a given namespace:

podSelector - selects a group of pods for which the policy applies
policyTypes -  defines the type of traffic to be restricted (inbound, outbound, both)
ingress - includes inbound traffic whitelist rules
egress - includes outbound traffic whitelist rules		
		


# We are applying network policy for mongo pods here. Only Spring app pods can connect mongo pods if we apply below rule.
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: test-network-policy
  namespace: test
spec:
  podSelector:
    matchLabels:
      app: mongo
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: springapp
    ports:
    - protocol: TCP
      port: 27017		
		
		



#########
EKS Setup
#########

1) Create IAM Role For EKS Cluster.
      EKS – Cluster 
2) Create Dedicated VPC For EKS Cluster. Using CloudFormation. 
     https://amazon-eks.s3.us-west-2.amazonaws.com/cloudformation/2020-08-12/amazon-eks-vpc-private-subnets.yaml 
3) Create EKS Cluster.
4) Create IAM Role For EKS Worker Nodes.
        AmazonEKSWorkerNodePolicy
        AmazonEKS_CNI_Policy
        AmazonEC2ContainerRegistryReadOnly -- > 
5) Create Worker Nodes.
6) Create An Instance (If Not Exists) Install AWS CLI , IAM Authenticator And kubectl. Configure AWS CLI using Root or IAM User Access Key & Secret Key. Or Attach IAM With Required       Policies.
      aws eks update-kubeconfig --name <ClusterName> --region <RegionName> 


####Setup K8s Client Machine #####

### Install Kubectl In Linux====

1) Install Download the latest kubectl release with the command:

curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"



2) Make the kubectl binary executable. 

     chmod +x ./kubectl
	 
3) Move the binary in to your PATH.

      sudo mv ./kubectl /usr/local/bin/kubectl
4) Test to ensure the version you installed is up-to-date:

kubectl version --client	 


### Install aws CLI In Linux====

1) Download AWS CLI ZIP
    
	curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

2) Download & Install Unzip
    sudo yum install unzip -y

3) Extract Zip 
    unzip awscliv2.zip
	
4) Install
	sudo ./aws/install -i /usr/local/aws-cli -b /usr/local/bin
	
5) Verify
  aws --version	
	
	
######## Configure AWS CLI using ACCESS Key & Secret Key ########

aws configure


##### Get KubeConfig file #####

aws eks update-kubeconfig --name <ClusterName> --region <RegionName> 

##### Verify Kubectl #####
kubectl get nodes
kubectl get pods



===== Cluster Auto Scaler Deployment in EKS========


1) Create AWS policy with below Actions .


{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "autoscaling:DescribeAutoScalingGroups",
                "autoscaling:DescribeAutoScalingInstances",
                "autoscaling:DescribeLaunchConfigurations",
                "autoscaling:DescribeTags",
                "autoscaling:SetDesiredCapacity",
                "autoscaling:TerminateInstanceInAutoScalingGroup",
                "ec2:DescribeLaunchTemplateVersions"
            ],
            "Resource": "*",
            "Effect": "Allow"
        }
    ]
}	  

2) Attach policy to IAM Role which is used in EKS Node Group.
	
3) Deploy ClusterAutoScaler using below yml(Make sure u update - --node-group-auto-discovery values with your cluster name under cluster-autoscaler deployment commands.)



apiVersion: v1
kind: ServiceAccount
metadata:
  labels:
    k8s-addon: cluster-autoscaler.addons.k8s.io
    k8s-app: cluster-autoscaler
  name: cluster-autoscaler
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: cluster-autoscaler
  labels:
    k8s-addon: cluster-autoscaler.addons.k8s.io
    k8s-app: cluster-autoscaler
rules:
  - apiGroups: [""]
    resources: ["events", "endpoints"]
    verbs: ["create", "patch"]
  - apiGroups: [""]
    resources: ["pods/eviction"]
    verbs: ["create"]
  - apiGroups: [""]
    resources: ["pods/status"]
    verbs: ["update"]
  - apiGroups: [""]
    resources: ["endpoints"]
    resourceNames: ["cluster-autoscaler"]
    verbs: ["get", "update"]
  - apiGroups: [""]
    resources: ["nodes"]
    verbs: ["watch", "list", "get", "update"]
  - apiGroups: [""]
    resources:
      - "pods"
      - "services"
      - "replicationcontrollers"
      - "persistentvolumeclaims"
      - "persistentvolumes"
    verbs: ["watch", "list", "get"]
  - apiGroups: ["extensions"]
    resources: ["replicasets", "daemonsets"]
    verbs: ["watch", "list", "get"]
  - apiGroups: ["policy"]
    resources: ["poddisruptionbudgets"]
    verbs: ["watch", "list"]
  - apiGroups: ["apps"]
    resources: ["statefulsets", "replicasets", "daemonsets"]
    verbs: ["watch", "list", "get"]
  - apiGroups: ["storage.k8s.io"]
    resources: ["storageclasses", "csinodes"]
    verbs: ["watch", "list", "get"]
  - apiGroups: ["batch", "extensions"]
    resources: ["jobs"]
    verbs: ["get", "list", "watch", "patch"]
  - apiGroups: ["coordination.k8s.io"]
    resources: ["leases"]
    verbs: ["create"]
  - apiGroups: ["coordination.k8s.io"]
    resourceNames: ["cluster-autoscaler"]
    resources: ["leases"]
    verbs: ["get", "update"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: cluster-autoscaler
  namespace: kube-system
  labels:
    k8s-addon: cluster-autoscaler.addons.k8s.io
    k8s-app: cluster-autoscaler
rules:
  - apiGroups: [""]
    resources: ["configmaps"]
    verbs: ["create","list","watch"]
  - apiGroups: [""]
    resources: ["configmaps"]
    resourceNames: ["cluster-autoscaler-status", "cluster-autoscaler-priority-expander"]
    verbs: ["delete", "get", "update", "watch"]

---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: cluster-autoscaler
  labels:
    k8s-addon: cluster-autoscaler.addons.k8s.io
    k8s-app: cluster-autoscaler
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-autoscaler
subjects:
  - kind: ServiceAccount
    name: cluster-autoscaler
    namespace: kube-system

---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: cluster-autoscaler
  namespace: kube-system
  labels:
    k8s-addon: cluster-autoscaler.addons.k8s.io
    k8s-app: cluster-autoscaler
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: Role
  name: cluster-autoscaler
subjects:
  - kind: ServiceAccount
    name: cluster-autoscaler
    namespace: kube-system

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: cluster-autoscaler
  namespace: kube-system
  labels:
    app: cluster-autoscaler
spec:
  replicas: 1
  selector:
    matchLabels:
      app: cluster-autoscaler
  template:
    metadata:
      labels:
        app: cluster-autoscaler
      annotations:
        prometheus.io/scrape: 'true'
        prometheus.io/port: '8085'
    spec:
      serviceAccountName: cluster-autoscaler
      containers:
        - image: k8s.gcr.io/cluster-autoscaler:v1.14.7
          name: cluster-autoscaler
          resources:
            limits:
              cpu: 100m
              memory: 300Mi
            requests:
              cpu: 100m
              memory: 300Mi
          command:
            - ./cluster-autoscaler
            - --v=4
            - --stderrthreshold=info
            - --cloud-provider=aws
            - --skip-nodes-with-local-storage=false
            - --expander=least-waste
            - --node-group-auto-discovery=asg:tag=k8s.io/cluster-autoscaler/enabled,k8s.io/cluster-autoscaler/EKS_Demo # Update Your ClusterName here
          env:
          - name: AWS_REGION
            value: ap-south-1 # Update Your Region Name here in which u have EKS Cluster
          volumeMounts:
          - name: ssl-certs
            mountPath: /etc/ssl/certs/ca-certificates.crt
            readOnly: true
          imagePullPolicy: "Always"
      volumes:
        - name: ssl-certs
          hostPath:
            path: "/etc/ssl/certs/ca-bundle.crt"
	    
	    

# App Deployment with Service of type Load Balancer
apiVersion: apps/v1
kind: Deployment
metadata:
  name: javawebappdeployment
  namespace: test-ns
spec:
  replicas: 2
  selector:
    matchLabels:
      app: javawebapp
  strategy:
    type: Recreate
  template:
    metadata:
      name: javawebapppod
      labels:
        app: javawebapp
    spec:
      containers:
      - name: javawebappcontainer
        image: dockerhandson/java-web-app:4
        ports:
        - containerPort: 8080
        resources:
          requests:
            cpu: 1
            memory: 512Mi
          limits:
            cpu: 1
            memory: 1Gi
---
apiVersion: v1
kind: Service
metadata:
  name: javawebappsvc
  namespace: test-ns
spec:
  type: LoadBalancer
  selector:
    app: javawebapp
  ports:
  - port: 80
    targetPort: 8080
    
### Another App With Service of type LB ####
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mavenwebapp
spec:
  replicas: 2
  selector:
    matchLabels:
      app: mavenwebapp
  template:
    metadata:
      name: mavenwebapppod
      labels:
        app: mavenwebapp
    spec:
      containers:
      - image: dockerhandson/maven-web-app
        name: mavenwebappcontainer
        ports:
        - containerPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  name: mavenwebappsvc
spec:
  type: LoadBalancer
  selector:
    app: mavenwebapp
  ports:
  - port: 80
    targetPort: 8080    	    






Ingress & Ingress Controller
###########################

Deploy Ingress Controller
-----------------------

git clone https://github.com/MithunTechnologiesDevOps/kubernetes-ingress.git

cd kubernetes-ingress/deployments
 
# Create a Namespace And SA 
kubectl apply -f common/ns-and-sa.yaml

# Create RBAC, Default Secret And Config Map
kubectl apply -f common/

# Deploy the Ingress Controller

kubectl apply -f daemon-set/nginx-ingress.yaml

# Check that the Ingress Controller is Running

kubectl get pods --namespace=nginx-ingress

# Create Service with the Type LoadBalancer for ingress controller

kubectl apply -f service/loadbalancer-aws-elb.yaml



# Define path based or host based routing rules for your services.

# Single DNS Name with Path
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: <name>
  namespace: <namespace>
spec:
  ingressClassName: nginx
  rules:
  - host: <domainName>
    http:
      paths:
      - pathType: Prefix
        path: "/<Path>"
        backend:
          service:
            name: <serviceName>
            port:
             number: <servicePort>

# Multiple DNS Name with Path	     
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: <name>
  namespace: <namespace>
spec:
  ingressClassName: nginx
  rules:
  - host: <domainName>
    http:
      paths:
      - pathType: Prefix
        path: "/<Path>"
        backend:
          service:
            name: <serviceName>
            port:
             number: <servicePort>
  - host: <domainName>
    http:
      paths:
      - pathType: Prefix
        path: "/<Path>"
        backend:
          service:
            name: <serviceName>
            port:
             number: <servicePort>
	          
		  
		  
# Single DNS with multiple paths

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: <name>
  namespace: <nsname>
spec:
  ingressClassName: nginx
  rules:
  - host: <domain>
    http:
      paths:
      - pathType: Prefix
        path: "/<Path>"
        backend:
          service:
            name: <serviceName>
            port:
             number: <servicePort>
      - pathType: Prefix
        path: "/<path>"
        backend:
          service:
            name: <servcieName>
            port:
	      number: <servicePort>
	      
example App:
----------
apiVersion: apps/v1
kind: Deployment
metadata:
  name: javawebappdeployment
  namespace: test-ns
spec:
  replicas: 2
  selector:
    matchLabels:
      app: javawebapp
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 1
      maxSurge: 1
  minReadySeconds: 30
  template:
    metadata:
      name: javawebapppod
      labels:
        app: javawebapp
    spec:
      containers:
      - name: javawebappcontainer
        image: dockerhandson/java-web-app:4
        ports:
        - containerPort: 8080
        livenessProbe:
          httpGet:
            path: /java-web-app
            port: 8080
          initialDelaySeconds: 30
          periodSeconds: 10
          timeoutSeconds: 5
        readinessProbe:
          httpGet:
            path: /java-web-app
            port: 8080
          initialDelaySeconds: 30
          periodSeconds: 10
          timeoutSeconds: 5
        resources:
          requests:
            cpu: 500m
            memory: 256Mi
          limits:
            cpu: 1
            memory: 512Mi
---
apiVersion: v1
kind: Service
metadata:
  name: javawebappsvc
  namespace: test-ns
spec:
  type: ClusterIP
  selector:
    app: javawebapp
  ports:
  - port: 80
    targetPort: 8080
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: javaweabppingressrule
  namespace: test-ns
spec:
  ingressClassName: nginx
  rules:
  - host: javawebapp.mithuntechdevops.co.in
    http:
      paths:
      - pathType: Prefix
        path: "/"
        backend:
          service:
            name: javawebappsvc
            port:
              number: 80
	      
# Another App
-------------
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mavenwebapp
  namespace: test-ns
spec:
  replicas: 2
  selector:
    matchLabels:
      app: mavenwebapp
  template:
    metadata:
      name: mavenwebapppod
      labels:
        app: mavenwebapp
    spec:
      containers:
      - image: dockerhandson/maven-web-application:1
        name: mavenwebappcontainer
        ports:
        - containerPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  name: mavenwebappsvc
  namespace: test-ns
spec:
  type: ClusterIP
  selector:
    app: mavenwebapp
  ports:
  - port: 80
    targetPort: 8080
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: mavenweabppingressrule
  namespace: test-ns
spec:
  ingressClassName: nginx
  rules:
  - host: mavenwebapp.mithuntechdevops.co.in
    http:
      paths:
      - pathType: Prefix
        path: "/"
        backend:
          service:
            name: mavenwebappsvc
            port:
              number: 80
	      


# Path Based Routing
---------------------
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: mithuntechappingressrules
  namespace: test-ns
spec:
  ingressClassName: nginx
  rules:
  - host: mithuntechdevops.co.in
    http:
      paths:
      - pathType: Prefix
        path: "/java-web-app"
        backend:
          service:
            name: javawebappsvc
            port:
             number: 80
      - pathType: Prefix
        path: "/maven-web-application"
        backend:
          service:
            name: mavenweabppsvc
            port:
	      number: 80



	      
# Ingress with Https Using Self Signed Certificates

openssl req -x509 -nodes -days 365 -newkey rsa:2048 -out mithun-ingress-tls.crt -keyout mithun-ingress-tls.key -subj "/CN=mithuntechdevops.co.in/O=mithun-ingress-tls"

# Create secret for with your certificate .key & .crt file

kubectl create secret tls mithun-ingress-tls --namespace test-ns --key mithun-ingress-tls.key --cert mithun-ingress-tls.crt


# Create ingress rules with tls secret create above.
-----------------------------------------------------
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: mithuntechappingressrule
  namespace: test-ns
spec:
  ingressClassName: nginx
  tls:
  - hosts:
      - mithuntechdevops.co.in
    secretName: mithun-ingress-tls
  rules:
  - host: mithuntechdevops.co.in
    http:
      paths:
      - pathType: Prefix
        path: "/java-web-app"
        backend:
          service:
            name: javawebappsvc
            port:
              number: 80
      - pathType: Prefix
        path: "/maven-web-application"
        backend:
          service:
            name: mavenwebappsvc
            port:
              number: 80




			 
========= RBAC With EKS IAM========================



As a Admin:
=============

1) Create IAM User With Polociy to List & Read EKS Cluster to get Kube Config File in AWS IAM Console.

2) Edit aws-auth to add userarn to aws-auth config map

  kubectl edit configmap aws-auth -n kube-system

apiVersion: v1
data:
  mapRoles: |
    - groups:
      - system:bootstrappers
      - system:nodes
      rolearn: arn:aws:iam::921483055369:role/EKS_Node_Role
      username: system:node:{{EC2PrivateDNSName}}
  mapUsers: |
    - userarn: arn:aws:iam::935840844891:user/Balaji          # Update your user arn here
      username: Balaji                                        # Update your user name.
kind: ConfigMap
metadata:
  creationTimestamp: "2020-10-19T03:35:20Z"
  name: aws-auth
  namespace: kube-system
  resourceVersion: "792449"
  selfLink: /api/v1/namespaces/kube-system/configmaps/aws-auth
  uid: 8135dcd1-90e6-4dfb-872f-636601475aca
	  
	  


## Create Role/ClusterRole & RoleBinding & ClusterRoleBinding#####


kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  namespace: default
  name: readonly
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get","list","create","delete","update"]
- apiGroups: ["apps"]
  resources: ["deployments","replicasets","daemonsets"]
  verbs: ["get","list"]
---
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: full_access_role_binding
  namespace: default
subjects:
- kind: User
  name: Balaji                           # Map with username
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: readonly
  apiGroup: rbac.authorization.k8s.io




Clinet Side:
===========
1) Install Kubectl & AWS CLI.

2) Configure AWS CLI(With Access Key & Secret Key of IAM User which you created in AWS IAM)

3) Get Kube-config file

   aws eks update-kubeconfig --name <EKSClusteName> --region <regionName>

4) try to access the cluster resources using kubectl
	      	      
Docker and Kubernetes roles and responsibilities:

Docker with Docker swarm
========================
Responsible for Dockerizing applications.
Configuring the Docker containers and creating Docker files for different environments.
Strong experience in writing docker files, docker compose files.
Responsible for configuring docker private registries to maintain docker images.
Responsible for creating & configuring docker volumes.
Responsible for creating docker swarm cluster and deploying docker services in docker swarm cluster.
Implemented CI/CD using Jenkins & docker swarm.


Docker with Kubernetes
========================
Responsible for Dockerizing applications.
Strong experience in writing docker files.
Responsible for configuring docker private registries to maintain docker images.
Responsible for creating Kubernetes manifest files like daemon sets, replica sets, deployments.
Responsible for creating & configuring  persistent volumes ,persistent volume claims.
Responsible for Kuberentes administrations tasks like settingup StorageClasses,creating Roles,ClusterRole,RoleBindings..etc
Strong experience in Kubernetes cluster setup and deploying applications in Kubernetes cluster.
Implemented CI/CD using Jenkins ,docker & Kubernetes.

AWS there will be a separate infra team who can mange infra for us. But if you are working or not working on AWS u can mention below on AWS. You 
can add more u know other services as well.

AWS
===
Good Experience in AWS Cloud Servcies like Ec2,ELB,VPC,EBS,,S3,EFS,IAM,AutoScaling,ECR,EKS.
Good Experience in creating VM's,networks,loadbalancers,storage services in AWS.
Automate, deploy, handle, and maintain cloud-based AWS  servcies.
Responsible for create EKS kubernetes clusters and ECR registries.
Responsible for taking back ups of ebs volumes.