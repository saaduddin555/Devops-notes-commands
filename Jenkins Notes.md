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