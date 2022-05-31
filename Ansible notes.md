# Ansible
Ansible is opensource configuration management and deployment tool which is maintained by redhat and Red hat is acquired by IBM
Configuration management is a set of task which are going to perfom in target server

The main components of Ansible are playbooks, configuration management, deployment

Ansible uses playbooks to deploy, manage, build test and configure anything from full server environments to custom compiled source code for applications

Ansible was written in python

Configuration can be any task which we can perform on server and hosts

It can be

Installing/update/ninstalling a software
Creating/deleting the users
copy files changing permissions o files and directories
Uninstalling the softwares
Start/stop or restart the services

We can automate the servers using Ansible

* Ansible is a push based Architecture
  There is no middle man or agent needed for ansible
  Basically Ansible is Agentless
  central erver pushes the configuration information on target servers
  you can control when changes are made into servers.

The chef/puppet are pull based architecture and agents are needed to configure the servers.

we can execute playbook using Ansible server to Host servers and perform Actions on host machines
The machines are configured to Ansible server using SSH Machine
The Ansible server will be always a Linux based OS

If the host and Ansible machines are in linux the connection type will be (SSH)
If the host machine is windows and Ansible server by default as Linux then Connection type will be (winrm)

Built on top of python hence provides a lot python functionality and Yaml based files
All playbooks are configured using YAML and YAML us human readable format.

If it is pull based it is going to check configuration in Main configuration server.

* We can use python language also instead of YAML to run the Ansible playbooks but we need python interpreter installed in all host servers so that they can understand python script but YAML is recognized by all servers, it doesnt need client.

* Ansible can be installed in local servers or public/private cloud, Once Ansible is installed we can see file called as HOST INVENTORY FILE
/etc/Ansible/host.........> 

we have two host inventory
1. static host inventory
2. Dynamic host inventory

In Static host Inventory : It conatins host machines which we are going to connect machines IP address or Domain name, The Manually updation of host inventory details

In Dynamic host Inventory: Automatically it will get update all the details of host servers, When we create AWS servers we will get all running server details in ansible inventory file.

* what is default path of host Inventory file /etc/ansible/hosts

* In this Host machines if you want to install a software or do some changes we write playbooks to do changes
we use YAML files to do changes

if we want to install JAVA software we use installjava.yaml or installjava.yml

# Ansible Architecture consist of:

* Host Inventory
* Playbooks
* Core Modules
* Custom Modules
* Plugins such as email, logging and other
* Connection plugins
* MAIN ANSIBLE area where we perform operation by users and where Users connect 

This whole is part of Ansible Server, where this server can be local or public/private
.
.
.
.
.
Host MAchines1 Host MAchines2 Host MAchines3 Host MAchines4 Host MAchines5 Host MAchines6 Host MAchines7 Host MAchines8 Host MAchines..N



# Some Core modules in Ansible are:
If we want to ping all the server we have ping server modules.

If we want to copy to a server we have copy module

If we want to execute shell scripts we have shell module

* If we want to write custom modules we should know PYTHON, Without Knowing Python we cannot write custom module.
Some AWS services like Lamda, BOTO3 these services also uses Python

* connection Plugins such as SSH and Winrm used to connect servers

* we are going to deal with HostInventory and Playbooks


# Installation of Ansible Server

The Host details are should be configured in Hostinventory file like IP address and Domain name of the server
There we have file called as hosts
In this file we are going to configure 

As how many server we have we need to configure.

Refer Installation document of Ansible in mithun technology website 

The default location for configuration file of Ansible is config file= /etc/ansible/ansible.cfg

ansible python module location: /usr/lib/python3.6/site-packages/ansible
executable locaton = /usr/bin/ansible

# How to communicate from Ansible server to host servers.
Password-less Authentication:
ssh-keygen ----------The Generated Public key i Ansible servers should be pasted in Host servers

TO paste into host servers directly from ansible servers

ssh-copy-id usr_name@<HostPrivateIP>   (Use private ip if the servers are in same VPC or network)

The SSH Public key which we have sent to other server will be copied in ~/ .ssh/authorized_keys

# where we need to store Host server details 
sudo vi /etc/ansible/hosts

copy and paste the host server IP address details in that file which you like to connect.

If we dont specify any connection type while pasting IP address, It will take default connection as SSH type.

we can all 100 of host servers ip address to hosts file so that to communicate to host server

Even we can differenciate the Servers which is for particular project Application and seggregate it seperatly 
in further will discuss how to do

# If we want to check connectivity from ansible server to all host server
ansible all -m ping

The -m Module ping converts to linux command and executes

If you see message "ping": "Pong"

The connection is successful


After restarting/stopping AWS server the server configuration in hosts file need not to change as Private IP is configured
As Private IP wont change and IF public IP is given the change occurs.

* To change to other user: sudo su -ansible

# How many core modules of ansible are Installed to check
ansible-doc -l
 Press Enter key to keep on loading the list
press q to come out of screen Q means quit.

# If you want to know more Information about module give module name
ansible-doc yum
ansible-doc ping

You can find module usage in ansible documentation also.

# if we want to install and perform operation in Ansible server as well as Host server
* Edit hosts file and mention ansible server IP or localhost if you are at same 
* This wont connect to localhost if you are performing operation from that server itself, Why because it uses Ansible configuration
and need SSH way of connectivity hence 
you need add SSH keys to your local server also to perform ansible tasks with in server.
TO do That:
ssh-copy-id username@localhost

To set password for a user if not set
sudo passwd user_name
Give password and hit enteer
retype password
TOkens updated Successfully.
===Local Host also connects successfully

# Execution of Ansible to servers using commands

* Using yum module we can install or uninstall the packages.

ansible ip_address -b -m yum -a "name=vim"
Using ansible to partiuclar ip address (-b means become as sudo) -m(means module) yum(it is a module name to install packages)
-a(it is attribute what to install) "name=vim" install vim package

ansible all -b -m yum -a "name=vim" (To install vim package in all servers which are configured with ansible host)

ansible all -b -m yum -a name="httpd"

Response: Changed=Installed 
Reponse: Success=Already installed

To Uninstall htppd package
ansible all -b -m yum -a name="httpd state=absent"   (If we dont specify any state it will gonna install it hence we specified state)

* shell Module
If host machine is not available or shutdown it wont connect or perform any action, which are running it will execute.

I Want to display servers up time

ansible all -m shell -a "uptime"

I want to display the date
ansible all -m shell -a "date"

I want to know Distribution name of Servers
ansible all -m shell -a "cat /etc/*release"

Which Os we are Using
ansible all -m shell -a "uname"

How much hard disk space is utilized 
ansible all -m shell -a "df -h"

When ever we are using options use "" double quotes or else it will give error

ansible all -m shell -a date
It will work without quotes here

ansible all -m shell -a df -h
It will give error as quotes is not given as options are present in command

Using Shell module we can execute the commands

Not every shell commands work in shell module as we have seperate modules for those commands such as ping module is available for ping Command

* service Module
To start service we use service module
ansible all -b -m service -a name="httpd state=started"

The httpd is started in all servers

To Uninstall htppd package
ansible all -b -m yum -a name="httpd state=absent"
(If we dont specify any state it will gonna install it hence we specified state and take as Present)

If you want to know more about using module packages with options like state and options visit ansible documentation.

we can use service module also as enable=yes or enable=no
weather service should start on boot or not

We use Playbooks generally to execute ansible commands insatead of ad-hoc commands.
We can learn more commands and explore it using Google or ansible documentation......

* copy module

It is used to copy the files and copy the directories we use the copy module, like scp command we do server to server copy and paste 

copy the file accross the host machines

ansible all -m copy -a "src=test.txt dest=/tmp/test.txt"
src=Local path to a file to copy to remote server This can be absolute or relative, if path is a directory it is copied recusively if path ends with "/" only insides conents of that directory are copied to destination.

dest=copy to destination directory to temp directory

ls -l /tmp
you will see file names in servers

* setup module

ansible all -m setup
It is getting all the machine properties, This properties are important to check the conditions, instead of all we can specift specific ip and check details

ansible localhost -m setup

These details are used when we want to check conditions

If it is a RedHat we are going to install this and that package, These facts we are going to use such conditions, mainly in playbooks and execute tasks.
Basically Host machine details it gonna give.

redhat we use yum
ubuntu we use apt 

# Group Servers
we have config host machine details and IP address in inventory file, Assume we have also installed application servers, database servers, other server 

we want to make it a group of servers like DB servers, App Servers like that
 we can specify in hosts file like

[dbservers]
ip address..
ip address...
ip address..

[Appservers]
ip address...
ip address...
ip address...
ip address...

we can classify groups like above
if we give ansible all, it will install packages to all servers
what if we specify and make it as groups and give names to it so it can execute to specific groups.

- If some servers are not related to any group we should keep at beginning of the host inventory file, or else it will consider those server  also if mentioned below
- #ipaddress makes a server ip as comment and unuse.....if you remove # it will uncomment the server.

- A hostname/ip can be member of multiple groups. as a application server might be webserver and also a db server too...

we can also use to configure like this 

appservers ansible_host=mithun-techno.appserver1.com ansible_connection=ssh ansible_port=5555

mailservers ansible_host=mithun-techno.mailserver.com ansible_connection=winrm

databaseservers ansible_hosts=mithun-techno.db.com ansible_connection=ssh

* How to Execute commands to particular group of servers
ansible dbservers -m ping
ansible Appservers -m ping

Instead of all use name of server in command to execute

Use can use all,groupname,hostname,ip adress to execute commands to that servers

* Inventory Parameters

ansible_connection=ssh/winrm/localhost
ansible_port=22/5986
ansible_user=root/administrator
ansible-ssh_pass=<<Password for node>>

for local host
localhost ansible_connection=localhost

if you want to have your Ansible hosts file in another location, then you set this Environmental variable:
If we want to configure our own host inventory file we can also configure our path like this
export ANSIBLE_HOSTS=/root/custom_ansible_hosts
Or you can specify the Ansible hosts locaton when running commands with the --inventory-file= (or -i) flag:

ansible all --inventory-file=/root/ansible_hosts -m ping

# Playbooks using YAML: YET ANOTHER MARKUP LANGUAGE

Use Ansble Documentation by Mithun Technologies to know more about YAML and Usage expalined in detailed...

Using Playbooks we can write Ennumber of Lines of Script to execute those tasks in servers.

Yaml file runs in Key:value pair 

Playbook is nothing but collection of tasks

In Yaml The indentation is Important.

Dont Use Tabs while using Indentation give space bars.


pingServers.yaml
---
- hosts: all|groupname|individualhosts
  tasks:
   - name: Ping Servers
     ping: 
...

# TO Execute Playbook file and also to check any eroor in YAML format
ansible-playbook pingServers.yaml
ansible-playbook pingServers.yml --syntax-check

# to check wheather we can install application or not validating the Drainer test
ansible-playbook pingServers.yml --check
we use this with application installation check...

# Connecting a server using PEM file also without config of SSH to host machines...In realtime we config SSH as per above notes
* Make sure pemfile is at path like /opt/aws.pem

172.31.35.23 ansible_user=ec2-user ansible_ssh_private_key_file=/opt/aws.pem

# TO get all Ansible playbook commands
ansible-playbook --help

gets all Playbook commands with options

























































