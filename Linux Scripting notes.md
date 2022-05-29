The first Line of Scipt always start with Shebang Line, which is also called as interpreter path of a programm where a programm can understand the code.

shellScript.sh

#!/bin/bash

echo "Welcome to bash script."
echo
echo "The uptime of the system is:"
uptime
echo
echo "Memory Utilization"
echo
free -m
echo
echo "Disk Utilization"
df -h

save the script in a file as shellScript.sh
./shellScipt.sh t run the script in command line

To give Xecute permmisions for a shell script 
chmod +x ./shellScipt.sh
.............................................................

# TO give Comments to script we use # symbol
like

#!/bin/bash

### This script prints system info ###

echo "Welcome to bash script."
echo

# Checking System uptime
echo "The uptime of the system is:"
uptime
echo

# Memory Utilization
echo "Memory Utilization"
free -m
echo

#Disk Utilization
echo "Disk Utilization"
df -h
.........................................................................

# Website setup Script without variables
Download a website from tublet.com
by f12 devlopers mode and....>>>>networks tab sections....Search for zip file...>>>>see zip file over there and copy the link of that web-zip artifact

Filename: website.sh

#!/bin/bash

sudo apt install wget unzip httpd -y

sudo systemctl start httpd
sudo systemctl enable httpd

mkdir -p /tmp/webfiles
cd /temp/webfiles

wget http://www.tooplate.com/zip-templates/2098_health.zip
unzip 2098_health.zip
sudo cp -r 2098_health/* /var/www/html

systemctl restart httpd

rm -rf /tmp/webfiles

.................................................................................................................................
# Using Variables writting a script for website setup

#!/bin/bash

# variables defined, Things that changes and varies and update and repeated task in script is used as variables,Just use Variables.

WEBSERVER="httpd"
URL="http://www.tooplate.com/zip-templates/2098_health.zip"
TEMPDIR="/tmp/webfiles"
ART-NAME="2098_health.zip"

sudo apt install wget unzip $WEBSERVER -y

sudo systemctl start $WEBSERVER
sudo systemctl enable $WEBSERVER

mkdir -p $TEMPDIR
cd /temp/webfiles

wget $URL
unzip $ART_NAME
sudo cp -r 2098_health/* /var/www/html

systemctl restart $WEBSERVER

rm -rf $TEMPDIR
...................................................................
# Remove files Script

#!/bin/bash
sudo systemctl stop httpd
sudo rm -rf /var/www/html/*   
# * defines all files in that folder to remove
sudo yum remove httpd wget unzip -y 
....................................................................
# command line arguments
Note: 0 is always reserved for the script name

we use command line arguments when we pass to system

example: mv shell.sh bash.sh
Here we have two arguments shell.sh and bash.sh 

we are passing an argument to command to rename a file from one to another.

In similar way we use command line arguments in bash shell scripting using numbers as mentioned in code and pass it in cmd line.

#!/bin/bash

echo "Printing script name"
echo $0
echo

echo "printing first argument"
echo $1

echo
echo "printing second argument"
echo $2

Save the file.

Type in command line to get results in shell script 
./arg.sh saaduddin shaik.

# The Output will print 0 as filename 1 as saaduddin and 2 as shaik 

Printing script name
./arg.sh

printing first argument
saaduddin

printing second argument
shaik

Another Example we can pass arguments like using commands instead of names
#!/bin/bash

echo "Archiving $1"
tar -czvf scripts.tar.gz $1

echo "Moving the archive to $2"
mv scripts.tar.gz $2

echo "Backup of $1 completed"
..............................................................................................................................................
# System variables
Some system Variables

There are few system variables that system sets for you to use as well

$0-The name of the Bash Scipt (As we have seen in command line arguments)
$1-9- The first 9 arguments to the bash script(As mentioned in command line arguments)
$#-How many Arguments were passed in bash script
$@-All the argumnts supplied to bash script
$?-The exit status of the most recently run process
$$-The Process ID of teh current script
$USER-The username of teh user running the script.
$HOSTNAME-The hostname of the machine the script is running on.
$SECONDS-The Number of seconds since the script was started.
$RANDOM-Returns a differnet random number each time is it refered to
$LINENO-Returns the current line number in the bash script.
.........................................................................................................................................
# Quotes
Quotes are used to refer a Variable 

Example: SKILL="DevOps"
echo $SKILL
DevOps

Example2: SKILL='DevOps'
echo $SKILL
DevOps

In both type of quotes the variable is working Fine

But in this Scenario

echo "I have got $SKILL skill."
I have got devops skill

echo 'I have got $SKILL skill'
I have got $SKILL skill

Here we are printing variable name itself not value in single quotes to solve this we use backward slash infront of a charecter to not consider it

echo 'I have got \$SKILL skill'
I have got DevOps skill

Another Example:

VIRUS="covid19"

echo "Due to $VIRUS virus company has lost $9 million."
output: Due to covid19 virus company have lost million

here $9 is not visible in command as we want to print

echo 'Due to $VIRUS virus company has lost $9 million.'
output: Due to $VIRUS virus company have lost $9 million.

hence to solve both of issues we use backward slash to indicate, The next special charecter will be ignored.
echo "Due to $VIRUS virus company has lost \$9 million."
output: Due to covid19 virus company have lost $9 million.
.......................................................................................................................................
# Command Substitution.
Variable defined in the script leave with it and dies after the script dies or completed. if we want to define a variable that is accessible to 
all the scripts from your current shell we need to export it.
Command substitution is method of storing Output of a command into a variable.

Uptime
Gives uptime of system

UP="uptime"
echo $UP
uptime

so to resolve and work a variable as a command use back ticks ``
UP=`uptime`
echo $UP
we will get command result

or

CURENT_USERS=$(who)
echo $CURRENT_USER
Gives output for the reult

free -m

              total        used        free      shared  buff/cache   available
Mem:           9480        4013        2497           6        2969        5203
Swap:          3072           0        307


free -m | grep Mem   (We have applied filters using this grep command)

              total        used        free      shared  buff/cache   available
Mem:           9480        4013        2497           6        2969        5203

awk command is a pattern scanning and processing language
By default it reads standard input and write standard output

so,

free -m | grep Mem | awk ' {print $4}'
Output:2495

So lets assign variable for this command 

FREE_RAM=`free -m | grep Mem |awk ' {print $4}'`

echo "The free space of ram is $FREE_RAM"

A Programm to Know Free space of Ram, Load , and Root Disk space.

#!/bin/bash
echo "Welcome $USER on $HOSTNAME."
echo "###########################################"

FREERAM=$(free -m | grep Mem | awk ' {print$4}')
LOAD=`uptime | awk ' {print $9}'`
ROOTFREE=$(df -h | grep '/dev/sda1' | awk '{print $4}')

echo "Availabe free Ram is $FREERAM MB"
echo
echo "Current Load Average $LOAD"
echo
echo "Free Root Partition size is $ROOTFREE"
................................................................................................................................
# Exporting variables
We Have how to store a string/text into a variable but sometimes you want to store output of a command to a variable. Like you may
need to store of its command output to a variable. For this we use Command Substitution.There are two syntax for doing this.

Export a variable

In Command terminal we have as assigned Variable as
SEASON="Mansoon"
echo "The $season is expected to be longer than usual"
Output: The Mansoon is expected to be longer than Usual

Create a shell script

#!/bin/bash

echo "The $SEASON is longer than expected 

save and run the script

./season.sh

output: The  is longer than expected

here if we see in output the variable which is defined outside in terminal is not assigned to shell script file, hence we export 
the variable 

export SEASON  WE NEED TO GIVE export VARIABLE_NAME Parent script to make it global use
as child script is not recognized earlier.

logout and login back

The varible is gone

if we want to make the variable permanent for specific users or any specific user go to
In every users home directory there is file called .bashrc or .bash_profile, if any root user login we can see this file and we can place commands there
source .bashrc
nano .bashrc
we can place commands over here, it will get executed
export SEASON="MANSOON"
source the file to refresh the data 
source .bashrc
You need to do it for every user profile to source the variable as normal user or other user cannot source it.

If we want to make a Global Access to variable, For Everyone Place it in to /etc/profile
This is global
Place the command here
export SEASON="SUMMER"
...........................................................................................................................................
# User Input

Taking Input from the user while executing the script, storing it into a variable and then using that variable in our script. we would be 
taking inputs from users like IP address,usernames,passwords or confirmation Y/N to do this we use command called read. Thos command takes 
the input and will save it into a variable.

#!/bin/bash

echo "Enter your Skills"
read SKILL

echo "Your $SKILL is in high Demand in IT Industry."

read -p 'Username: ' USR
read -sp 'Password: ' pass

echo 

echo "Login Successfull: Welcome USER $USR,"

Here as per above read statement is used to take input from user. and USR is defining as variable for username and same as password.

read -p means -p IS PROMPT
READ -sp means Promt with no visibility of text
....................................................................................................................
# If Statements
Scripts can make decisions.
Basic If Statements

If you use bash for scripting you will undoubtedly have to use conditions a lot. Based on a condition you decide if you should
execute some commands on the system or not. A basic if statement effectively says, if a Particular test is true, Then perfom a given set of actions. If it is not true then dont perform those actions. If follows the format below:

# if
#!/bin/bash

read -p "Enter a number: " NUM
echo
if [ $NUM -gt 100 ]
then
    echo "We have entered in IF block."
    sleep 3
    echo "Your Number is greater than 100"
    echo
    date
fi

echo "Script execution is completed successfully."

# else
#!/bin/bash

read -p "Enter a number: " NUM
echo
if [ $NUM -gt 100 ]
then
    echo "We have entered in IF block."
    sleep 3
    echo "Your Number is greater than 100"
    echo
    date
else 
  echo "Yo have entered number less than 100."
fi

echo "Script execution is completed successfully."
...........................................................................................................................................
# Else if - CONDITIONS

ip addr show | grep -v LOOPBACK | grep -ic mtu
here -ic means count of mtu times it repeated in ip addr show

#!/bin/bash

value=$(ip addr show | grep -v LOOPBACK | grep -ic mtu)

if [ $value -eq 1 ]
then
  echo "1 Active Network Interface found."
elif [ $value -gt 1 ]
then
  echo "Found Multiple active Interface."
else
  echo "No Active interface found."
fi

Here the script tells us how many times it got repeated if it is repeated 1 -eq eual to 1 print 

if it is -gt greater than 1 means if the values are 2 then print FOunf multiple

or if it is zero then no active is found.
............................................................................................................................................
# Monitoring Script

! Expression                The Expression is false
-n STRING                   The length of String is greater than zero
-Z String                   The length of string is zero that is empty
STRING1 = STRING2           The string 1 is equal to string 2
STRING1 != STRING2          STRING1 is not equal to STRING2
INTEGER1 -eq INTEGER2       Interger 1 is numerically equal than Integer 2
Integer1 -gt Integer2       Integer1 is numerically greater than Integer 2
Integer -lt Integer2        Integer1 is numerically les than Integer2
-d FILE                     File exist and is a directory
-e File                     File exist
-r File                     File exist and the read permission is granted
s File                      File exist and its size is greater than zero
-w File                     File exist and the write permission is granted
-x File                     File exist and the execute permission is granted
-f File                     File exist or not

0 Means True in bash scripting 
Non 0 means false which is 1

echo $?

systemctl status httpd
When ever the process is running there will be pid file get created.
if httpd is unning there will be pid file
if process is dead there will not be any file
hence if we go to path of httpd 
cat /var/run/httpd/httpd.pid
No such file or directory
echo $?
1
hence we will create a script where we will know when a process is running or not 

#/bin/bash
echo "#################################"
date 
ls /var/run/httpd/httpd.pid &> /dev/null

if [ $? -eq 0 ]
then
  echo "Htppd process is running."
else 
  echo "Htppd process is Not unning."
  echo "starting he process"
  systemctl start httpd
  if [ $? -eq 0 ]
  then
    echo "process started sucessfully."
  else
    echo "Process starting Failed, contact the admin."
  fi
fi
echo "#######################################"
echo

In above if syntax we can use also as if [ -f /var/run/httpd/httpd.pid &> /dev/null ] instead of if [ $? -eq 0 ] as the -f operator checks file if exist or not and need to remove ls line in the script.
.....................................................................................................................................
# Loops

Execute the task again and again and save the time, For loops runs in sequence.

#!/bin/bash


for VAR1 in java .net python ruby php
do
  echo "Looping....."
  echo "###################################################"
  echo "Value of VAR1 is $VAR1."
  echo "###################################################"
  pwd
done

echo "Out of for loop"
date

#!/bin/bash

# Looping over 1 2 3 4 5
echo "####################################################"
echo "Looping over 1 2 3 4 5"
echo "####################################################"
for i in 1 2 3 4 5
do
   echo "Welcome $i times"
done



# Looping over range 1-5
echo "####################################################"
echo "Looping over range 1-5"
echo "####################################################"
for i in {1..5}
do
   echo "Welcome $i times"
done


# Looping over range 1-5 using seq command
echo "####################################################"
echo "Looping over range 1-5"
echo "using seq command"
echo "####################################################"
for i in $(seq 1 5)
do
   echo "Welcome $i times"
done

# Looping and incrementing variable value
echo "####################################################"
echo "Looping and incrementing variable value"
echo "####################################################"
for (( c=1; c<=5; c++ ))
do  
   echo "Welcome $c times"
done

echo "Script exec completed."
.......................................................................................................................................

# ssh-keygen

ssh devops@web01 uptime 
it will ask password
enter password u get the reply
hence to avoid
use 
ssh-keygen
(/root/.ssh/id_rsa):
It is the place where public key and private key is stored
The public key is is called as Lock
and Private key is called as Key

Lock and key

The lock should be applied on web01 
hence 
ssh-copy-id devops@web01
like that u can copy to all the users
enter password

remote execution
The password wont be asking now because ssh is usisng default key which is present in id_rsa

what is it actually doing is it is trying to connect as ssh -i .ssh/id_rsa devops@web01 uptime
it is using key to login to machine in this command
...........................................................................................................................................
# cronjobs

mm HH DOM mm DOW 
minute                   30 min
hour                     20 hour
date of month            4
month                    jan
day of week     0means sunday 1-monday 2-tuesday .........6-saturday
                        1-5 means monday to friday
* Indicates Null

cron job be like

30 20 * * 1-5

Mon to friday 8:30 evening will run the job.
.......................................................................................................................................

# shell Scripting (Part 2)

cat /etc/shells              To know what type pf shells does os supports, gives list of various shells.

echo SHELL
SHELL

ECHO $SHELL
$SHELL is a Variable it contains Shell type value
/bin/bash

If u want to switch from one shell to another , Just type in command line
$/bin/sh
$/bin/bash

echo $0
/bin/bash

ps -p $$
gets Shell Type

What is a shell scripting 
It is a simple file which contains series of commands
All the shell script extensionn end with is .sh
hello.sh
if .sh extension is not given to shell script still it is going to work

serverresourcesmonitor.sh

CPU
RAM
HDD

THRESOLD=80
free
df -h
top
mail
ifconfig
hostname

Now we are using monitoring tools.

*/1 * * * * /home/ec2-user/hello.py
It will execute cron job for every minute

dbbackup.sh
deploy.sh
cleanup.sh

#!-----------Shebang
#!/bin/bash ---------------Shebang line
What ever the commands which we give these commands one by one will read and execute to the operating system
Shebang line is not mandatory bcoz the default shell type will be bash
hence if we want to execute other shell type we need to represent the shebang line

If we want to execute the shell script, we should give the execute permissions.
chmod u+x hello.sh
After giving xecute permissions, how to run a shell script
./hello.sh
. hello.sh
sh hello.h
bash hello.sh
csh hello.sh
zsh hello.sh

# Debug Mode
Why we need to run a shell script in debug mode
If we are getting errors, why we are getting error hence we run shell script in debug mode
sh hello.sh---------->Normal Run
sh -x hello.sh-------->Debug Mode

In debug mode we can easily identify what is wrong happening in the script which is not executing

If you want to run specified lines in debug mode

#!/bin/bash
echo "Hello Everyone"
echo "GM/GA/GE"
set -x
echo "Today date is"
set +x
date
echo "welcome to first shell script"

The lines which we want to execute in shell scripts should be mentioned in between such as 
set-x(Start the debug mode)and set +x(stop the debug mode)

# File naming conventions:
A file name can be maximun of 255 charecters
The name may contain alphabets, digits, dots and underscores
system commands or linux reserve words cannot be used for file names
file system is case sensitive
linux commands should not be used as shell naming and few keyword which are iternal part of system
some of valid filenames in linux are

syed.sh
Syed_saaduddin.sh
Saad0123.sh
Syed.sh
All the linux commands are lower case
options might be lowercase or upper case

# Comments
Comments make understandablity and readability of the source code
* single line comment represented by symbol #

* Multiline Comment 
<<Give any name 

Give

What ever string u have given same thing should be given at end to represent Multiline comment
All these line will be ignored by interpreter.

# Variables

System defined Variables 

How to check system defined variables
Commands:
env
printenv
echo $SHELL
echo ${SHELL}
To execute a variable value we should use $ symbol infornt of variable name.

PWD- upper case PWD is system defined variable
pwd- Lower case pwd is a command.

how to change a variable value temporarly for system defined variables
echo $HISTSIZE
1000
export HISTSIZE=200
echo $HISTSIZE
200

~ Is used to represent home directory
~/.bash_profile
The bash profile helps to store VARIABLES to that particular user only for other users they need to change in thier bash profile
if want to make HISTSIZE TO 200 PERMANENTLY for that user
Just open .bash_profile
and save variable in that profile
export HISTSIZE=200
This will save variable for that User 

To Define Variable for all Users
nano /etc/profile
export HISTSIZE=200
AND SAVE IT
This Variable will work for all the Users

These variables used in shells scripts also.


User defined Variables:
These variables are defined by user and can execute in temporarly or permanently as per above steps

How to switch User in linux: sudo su - username


In Shell script we dont have data types
creating a variable and assigning a value is called as Initialization.

The variable name and value should not contain any spaces in shell scripting.

a=10
b=20
Name=Syed

echo "a variable value is: " $a
echo "b variable value is: " $b
echo "name variable value is: " $name

How to use system defined variable to a variable again or
How to use a variable as a variable which is assigned as a variable earlier.
 
$PWD is a system defined variable

To use this variable again as a variable 

presentdir=$PWD
echo "Print the current dir is: " $presentDir
echo "The User name is: " $USER

hence the $presentdir is a variable which calls another variable $PWD and gives output

Always create userdefined variables in lowercase as best practice, iF we create userdefined variables as Upper case we wont get any error
If it is a system defined variable it will be in UPPER_CASE 
so to differenciate we use this as best practice.....

Always a variable will consider a updated value
a=10
a=40
Because the shell script executes step by step

in this scenario
# scenario 1
a=10
b=20
a=40
Name=Syed

echo "a variable value is: " $a
echo "b variable value is: " $b
echo "name variable value is: " $name

It will take a=40 

# Secnario-2
a=10
b=20
Name=Syed

echo "a variable value is: " $a
a=40
echo "a variable value is: " $a
echo "b variable value is: " $b
echo "name variable value is: " $name

Here the first line it will take as a=10
The second $a will take it as 40 as it was declared after passing the output


# Command Line Arguments:
Commands line arguments are such which is used while passing the shell script

Here two arguments is passed in this command line execution of script with arguments

bash shellscript.sh dbname dbbloc

How to get command line arguments and how to use it

echo $0  will use script name 
If we want to use first argument use 
$1
if we want to use second argument use
$2

echo $0 -----scriptname
echo $1 -----1st arg
echo $2 -----2nd argument
echo $9 -----9th argument

if value is more than 1 digit keep argument in flower brackets or else it will not understand and consider as 1st argument
echo ${10}
echo ${11}

echo $# -------Number of arguments to pass

echo $* -------All the Arguments as a one string

echo $@ -------All the arguments each argument as one  one string

If we execute any command or shell script in linux a process id is created PID

how to see process id 

echo $$ ------PID of the script
ps command process id which are running in users

date
echo $? --------previous command execution status
if the previous command executed successfully it will give result as 0

Date
echo $? --------previous command execution status
Command not found
echo $?
127  eroor is standard eroor for coomand not found.

we can specify n number of arguments, there is no limitation
Each argument is seperated by space

#/bin/bash

echo "C L Arguments Demo"

echo $0
echo $1
echo $2
echo $3
echo $4
echo ${10}
echo $#
echo $*
echo $@
echo $$
date
echo $?

execution: sh dbbackup.sh facebook amazon /tmp  

How to execution a script if two arguments are met....

if [ $# -eq 2 ]
then
echo "C L Args Demo"

echo $0
echo $1
echo $2
echo $3
echo $4
echo ${10}
echo $#
echo $*
echo $@
echo $$
date
echo $?

else
echo "Please pass the two argumennts
echo "usage: sh $0 arg1 arg2"
fi

bash shell.sh facebook
The condition is not met hence the arguments wont pass as one condition is given in arguments
hence it will state erorr as else
Please pass two arguments 
with $0 as filename and to give arg1 arg2

bash shell.sh facebook amazon
here two arguments passed hence the script will execute.

-eq ---------------- ==   equal
-ne ---------------  !=   Not equal

le ---------------- <=    less than or equal to
lt ---------------- <     less than
ge ---------------- >=    greter than or equal to
gt ---------------  >     greater than

TOMCAT/SONARQUBE/NEXUS/JENKINS needs java to run

I want to know how to find java version is installed or not in system, write a shell script

Steps:

java --verison
if [ $? -eq 0 ]
echo "Java has Installed
else
echo "Java has not installed"
fi

# String

name="It is considered as string"
if it is a single quote '' or "" double quote it will be considered as a string.

location='Bangalore'

string_var="Hi Team, My name is Syed, Working in Flipkart, Embassy Tech village"
string_variable=value

echo $string_var

echo ${string_var}

if you want to find string size and length
In java and python we have a function to find out, but here we dont have those set of libraries to find out
then 
we have to use some special charecters

echo ${#string_var} ---------It will give length of var

if we dont give # it will be going to display the value

# if we want sub string 

Hi Team, My name is Syed, Working in Flipkart, Embassy Tech village

how many charecter we dont want we can ignore it by
spaces,comma is also considereed

first 20 charecters i dont want to display the code is
echo ${string_var:20} -------------------it will ignore first 20 and show the rest
This ignores first number of charecters

echo ${string_var:20:10}
This wll ignore first 20 charecters and shows reset 10 charecter if some thing is there after 10 charecter those will also ignore.
This helps to show middle charecters and ignores first and last or the rest 10

If you want to display last 8 charecters of a string.
echo ${string_var: -8}
or 
echo ${string_var: (-8)}

If you want to show first 2 charecters of a string Then,
echo ${string_var:0:2} 

# Arthemetic operators

+ add
- sub
* Multiplication
/ Division
% percentage

If you want to perfoem arthemetic operators use "expr" keyword
Need to give spaces when performing Arthemetic operations

expr 2 + 3
expr 2 - 3
expr 2 \* 3  use backward slash as escape charecter or else it will consider as a special charecter
expr 10 / 2  
expr 20 % 3  modular 

*  asterisk
~  Tilda
`  Inverted comma, Back quote
,  comma
'  single quote
"  Double quote
/  forward slash
?  question mark
.  dot
:  colon
;  semicolon
{}  Flower Brackets
[]  brackets, square brackets
/   Forward Slash
\   Backward slash
=   Equal 
(   open parenthesis
)   Close parenthesis
!   Exclamation mark
@   at, at sign 
#   Hash
$   dollar
%   Percent sign
^   carat, hat, circumflex, exponent symbol
<>  Angle brackets
<   less than
>   greater than
&   and, ampersand
*   asterisk
-   minus
_   underscore
|   vertical pipe


#/bin/bash

a=2
b=5

echo "Adding the numbers is: " `expr 2 + 2`

echo "Adding the two numbers: " `expr $a + $b`

#always give space between operators and numbers or else there will be error in script

if you are giving command in between script use `Inverted commas` like above

* Using command line arguments
#/bin/bash

expr $1 + $2
expr $1 - $2
expr $1 \* $2
expr $1 / $2
expr $1 % $2

bash arth.sh 10 20

# Read comment 

echo "Please enter your name.."
read personName
echo "The name which you have given is: " $personName
...............................................
#bin/bash

echo "Enter number to perform arthemitic operation: "
read numb1

echo "Enter the second number: "
read numb2

expr numb1 + numb2
.....................................
#bin/bash

echo "Please enter the Devops tools: "
read DevOpstools

For example:(#The devops tools which user is given is git jenkins maven tomcat docker kubernetes)

echo "The devops tools which you have typed is: " $DevOpstools
................................................
# Array
It is group of memory locations where we can store same data types
In shell scripts there is no datatypes

In array the data is stored in sequnece like 0  1   2  3   4  5  6  7  8 .............n number of times

0     1             2      3         4          5
git   Jenkins     Maven    Tomcat   Docker    Kubernetes

if we want particular output of a tool instead of all, use array Instead of giving variables.
Example:

* Array method

#/bin/bash

echo "Please enter devops tools: "
read -a DevOpstools

echo "The Devops tools which you have given is: " ${DevOpstools[*]}
echo "The 4th element is: ${DevOpstools[3]}

Here in this script the array values which is mentioned in [*] means all values as output
The array values which is mentioned in [3] means to give values which is present in array 
as per above the [3] array value is Tomcat which is 4th element as array starts with "0"

# Without Variable name or array name

echo "Please enter devops tools"
read 

echo "The Devops tools which you have given is: " $REPLY

$REPLY is a inbuilt system variable which gives output

# Here as per above the input is asking in next line but i want input in same line so

read -p "please enter the username: " userName
read -p "please enter the password: " password

echo "The User name which u have type is: " $userName
echo "The password which u have type is: " $password

How to hide a password, without visibility
read -sp "please enter the password: " $password

The -sp will hide the password visibility

# Input output redirection symbols

>   ---- Redirect standard output

>>  ---- Append the std outut

<  ----  standard input

ls > lsopt.log
The command will redirect the output as in a file
if the file is not exist still it will create a new file

date > lsopt.log
The command will redirect and overwirite as it is already available as above scenario, it will erase ls output and overwrites date output

ls >> lsopt.log
This will not overwite and preserve previous outputs and further data when we mention the file_name.

cat < lsopt.log
The lsopt.log file gives input to cat 
By default it happens, if you dont specify it as a part of os programme
we give input symbols in jenkins alot

* I want to redirect output to a particular file and error in console itself
Lets take an example of script where it as output and eroors also 
sh shellscript.sh loc > shellbackup.log
This command will give output in file and error in command line itself.

# File descriptors: as per below scripts usage examples
0 -------standard input
1 -------standard output
2 -------standard error

* The output in one file and error in another file
sh shellscript.sh loc 2> error.log 1>output.log

* I want to redirect both error and output into a file
sh shellscript.sh loc > shellbackup.log 2>&1

# If Else condition
Syntax:
if condition
then
   Display commands list if condition is true
else
  Display commands list if condition is false
fi

Note: if and then must be seperate with a "New line" or a semicolon(;). The termination of if condition is fi

#/bin/bash

a=10
b=20

if [ $a -gt $b ]
then
echo "$a is bigger than $b"
else 
echo "$b is bigger than $a"
fi

Write a shell script to get the file name from the user and check weather file is existed or not?

#/bin/bash
echo "Please type the file name which you want to search"
read filename

#if we dont specify the path it will search in present directory, hence i have given path /opt/ and -f means file
if [ -f /opt/$filename]  
then
echo "$filename is existed.."
else
echo "$filename is not existed.."
fi

#/bin/bash
echo "Please type the file name which you want to search"
read filename

#if we dont specify the path it will search in present directory, hence i have given path /opt/ and -f means file
if [ -f /opt/$filename]  
then
echo "$filename is existed.."
echo "$filename contents are.."
cat $filename
else
echo "$filename is not existed.."
echo "$filename is creating.."
touch $filename
fi


# Nested if else condition, if, if conditions are more than two

a=10
b=20
c=30

if [[ ($a -gt $b && $a -gt $c) ]]

If there are more than two conditions, you have to keep two square brackets as above and concondition is mentioned in()

for complete code refer documentation of linux shell scripting or google.

# For loop

we use loops to satisfy conditions as long as conditions are met

* write a shell script to print the number s from 1 to 5

#/bin/bash

echo "For loop demo starts..."

for (( a=1; a<=5;a++ ))      ((Initialization,condition,Increament or decrement)) should be in body               
#Initialization is process of creating the variable and assigning the value.
#a++ is incrementor operator as a value increases untill condition meets
do
echo $a
done

echo "For loop demo over"

Write a shell script to print the numbers from 100 to 1

Assignement to do

# While loop

Initialization

While [ Condition ]
do
.....
inc/dec

done


#/bin/bash
echo "While loop demo starts.."
a=1

while [ $a -le 5]
do
echo $a
a=`expr $a +1` 
#we can use as a++ also instead of expr operator
done
echo "While loop demo over.."

What is the difference between for loop and while loop
Here we wont see that much difference in shell script for for and while loop.

# Switch Case

Switch case is alternative for nested if esle

if we want to check multiple conditions we use switch case

sh sonar.sh restart or stop or start 
#we can give any command line arguments for this script

#/bin/bash

case $1 in

start)
#Usally we can give commands here to start the server
#when user passes start after name in command line arguments these commands should execute is what it means here
echo "sonarqube server is starting"
echo "sonarqube server is started"
;;

#To end Switch case we need to use ;; symbol for every end of switch case.

stop)
echo "sonarqube server is stopping"
echo "sonarqube server is stopped"
;;

restart)
echo "sonarqube server is restarting"
echo "sonarqube server is restarted"
;;

*)
#we can use this switch case as * when user is not passing proper switch cases like example user might use upper_case letters
echo "please pass the correct pattern"
echo "Usage: sh $0 start|stop|restart"

esac
.....................................

#/bin/bash

echo "Please type the numbers from 1 to 5"
read numb

case $numb in
1)
echo "you have typed one."
echo "Typed the correct number.."
;;
2)
echo "you have typed two ."
echo "typed the correct number.."
;;
3)
echo "you have typed three ."
echo "typed the correct number.."
;;
4)
echo "you have typed four ."
echo "typed the correct number.."
;;
5)
echo "you have typed five ."
echo "typed the correct number.."
;;
*)
echo "Invalid Number"
echo "Please pass the numbers from 1 to 5 only.."

esac

# Functions

To avoid duplicate set of commands or work we use functions

What ever the commands which we use repeatedly keep that in functions. and call that functions in the script

functionsdemo.sh

greetfn(){
echo "Hello Everyone"
echo "GM/GA/GE"
echo "Functions are useful to resuse the code.."
}

echo "Functions are very imp.."
echo "using the functions we can stop the duplicating the code"

Here in above script we have defined functions, but we did not call functions any where in script so it will execute the rest part of code.


#calling the Function in this script

#/bin/bash
greetfn(){
echo "Hello Everyone"
echo "GM/GA/GE"
echo "Functions are useful to resuse the code.."
}

echo "Functions are very imp.."
echo "using the functions we can stop the duplicating the code"

echo "calling the function"
greetfn


#Function should always be like, Functionname(){ and closing should be } or else it will consider as command
#if you just five greetfn  for function greet(){       

#}
............................................
we can import functions from one script to another script using file name of script
Assume functions script in Utilities.sh

utilities.sh

#/bin/bash

add(){
  echo "I am from add function"
}

sub(){
  echo "I am from sub function"
}


arthmetich.sh

#/bin/bash
source ./utilities.sh
#we use ./filename when file is in current directory, if not we need to give path, here . represents current directory

add
sub

it will call the function and execute the script.
............................................................................................................................................

























































































































































































































































































































