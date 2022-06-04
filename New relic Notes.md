# NewRelic

There are two types of monitoring tools 

Application Monitoring tools such as 

Newrelic
Prometheus
grafana
Nagios
cloudwatch for AWS

Log Monitoring tools
The Log entry monitoring toold going to monitor just the log entries and error of the infrastructure.
Splunk
ELK Stack 
Elastic Search, Logstash, Kibana

The Newreic is a SAAS based Software as a Service.
Which we dont need to Install or create a server.

Newrelic website

https://newrelic.com

Create account and click on sign in and you see dashboard page 

SO if you want to monitor the application such as Tomcat we use Newrelic to monitor

# Rest API

The RestAPI response is always in JSON format

The REST API functionality is to call server and interract it using programmitically way

jsonlint.com, A website Place where we can validate json format.

If we want Temperature details in your app we use URL ENDPOINT of REST API, The REST API Url and endpoint which gives response as a data.

Assume Rest API is developed by using Python, it can be developed by any language.

The rest api which we have in temperature site is devloped by Python

can we have that restAPi in our .Net project????

As language is different

YES, we can able to call temperature service, Once if you call REST API we get Json as Output, IT can read the data and display as Output.

# Assume if we want to monitor that REST API service.

SLA- (90% we have provided high Availability of APP), The rest 10% is Uncertainity of Infrastructure

The AWS is giving SLA(Service level Agreeement as 99.9%. They are going to give availability of services.

Not Every one can assure 100% of SLA to client..

Clients have Agreemet with Companies about SLA being Availabilty of the Application.

Hence we need to give data related to Availability of Application

Thats is Why we need to carefully Monitor the Server and give data to clients that the service was available..

If any issues we need to immediatly fix the issues..

As being human being, it is hard to monitor the apps and REst API's whether they are performing or not..

* In NEW RELIC we have Synthetics tab where you can Monitor the Application.

----Create your First Monitor
Find the problems before they reach to customer 
simulate the user traffic to detect an resolve outages and performance problems with URLS and APIs and critical services. Create a synthetic monitor.

-----Choose your Monitor type
Ping                           we can ping the URL and REST API
simple browser                 we can monitor the APP website by full page load and provides deep insights like resource breakdown and timelines.
scripted browser               we are going to use when it want navigate the application
API TEST                       API Test monitor uses an http client to monitor remote API endpints (REST/healthcheck/etc)


-Enter the details
-Firstname of Monitor 
-Enter a Url of that API
-Add a monitoring string to look in reponse       Response validation always should be related to string of url or leave it empty.
-Enter monitor locations                         (Give locations of clients and where you want to monior the API)

The Devlopment Team will give data which URLS we want to going to Monitor and which locations also...

We need to Just configure it..

Set the Schedule
1 Min schedule is for 24hr service

Create Monitor

From Now on wards it will Monitor that API and it will also monitor how much response it is taking to load that link..

The load time differes from region to region depends up on deployment location of that application server location...

If the server is deployed in Mumbai region The latency to load will be lesser compare to other locations...

* Assume US people are complaining about the services and load time is less 
 Tell me how can you resolve this issue..

 We are going to identify in which regions our clients are there...

 we will be deploying the applications where our clients are if in USA,UK,Germany all three we deploy

 we will be configuring our application servers using Elastic Load balancer.

 If the request is comming from UK client the Aplication will Route to UK server
 If the request is comming from USA client the Application will be routed to USA server


In Dashboard we can see Slowest regions also, How much time it is taking to call that API

In Dashboard we can see failure sections also is there any failures to call that service

We can filter by timeline by clicking filter at right handside....like 30 min, 7days, etc...

* If we configure we can send notification to slack channel and Email also..

# You can give As number of API's to monitor

General.....For settings 

# Unprotected API
 The API which is not required to provide credentials to acess is called unprotected API
WE USE PING monitor for unprotected API

# protected API
There are protected API Url also to onitor such we need to provide credentials also.
We are going to use API TEST.

### Infrastructure Monitor

Hosts means server

AWS

GCP

AZURE

Kubernetes 

All other servers are monitored

Add your first host and configure teh Rest ................


Just and Overview...


Prometheus and Grafana is used alot now a days for monitoring....as Opensource tool..





 

