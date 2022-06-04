# Linux 

In Linux we have various flavours such as 
* Red hat
* Cent os
* Ubuntu
* Suse Linux
* fedora
* Gentoo
* debiam 
* slack ware

The pre requsiste softwares used for linux to connect systems are:
* Putty 
* super Putty
* Mobexterm

The FTP Tools are in need to transfer the files from server to another are
* Win SCP
* Filezilla
* Cyberduck

# Intoduction to linux

Introduction
§ Linux started around 1991 by Linus Torlvads.
§ Linux is an multi-user, multitasking Operating System.
§ Linux is Open Source not like AIX , Sun Solaris, HP-UX...
§ Linux is “case-sensitive” ls is different of LS. 
§ Following are the Linux distributions.
1) Redhat
2) CentOS
3) Ubuntu.
4) SuSe Linux
5) Fedora
6) Gentoo
7) Mandriva.
8) Debian.
9) Slackware

# Linux File structure

Linux file system is casesensitive. (Mithun and mithun both are different)

Hidden files start with . (dot) extension.

dot (.) refers to current dir.

Following are the directories in the Redhat OS.
/ called is root directory.

home : It contains home directories for all users to store their personal files.
Ex: /home/bhaskar or /home/mithun

bin : It contains the commands and binary files. User can access the commands.
Ex: mkdir, ls, cd, ps….

sbin : Just like /bin It contains the commands and files, but only root user can access.
Ex: ifconfig, reboot, shutdown and swapon …

etc : It contains the configuration files. 

lib : It contains the system libraries.

proc : It contains the process information. 

tmp : It contains the temporary files.

usr : It contains the binaries and libraries. WAS,IHS or DB2 etc related softwares will install in 
this directory.

var : It contains variable files. This includes system log files(/var/log), emails (/var/mail) and 
temp files needed across reboots (/var/tmp)

dev : It contains the device files. 
Ex: USB or any device attached to the server

Questions:

# How to Know how many users are created in Linux server
--> Go to home directory and you will find how many users folders are there..
Users Directory is Equal to Home Directory in Linux

# In Sbin directory what S stands For?
-->S stands for System Bin

# What is the difference between Bin and Sbin ?/
---> Type of Users in Linux Os..
/ Root User or Admin or Super User
Normal Users


# Differnet types of commands

Navigation and Directory Control Commands
§ mkdir : Make or Create directory
§ ls : List the directory contents. 
§ tree: It will list contents of directories in a tree-like format.
§ cd : Change directory 
§ pwd : Print working directory 
§ rmdir : Remove or Delete directory 
§ rm : It will remove a file or directory.


Command in Linux Command in DOS
mkdir          md & mkdir
ls             dir
cd             cd (OR) chdir
pwd            cd
rmdir          rd & rmdir
cd             cd


File Maintenance Commands
§ touch :It will create the file with zero bytes.
§ find : find command used to search and locate list of files and directories based on conditions 
you specify for files that match the arguments. Find can be used in variety of conditions like 
you can find files by permissions, users, groups, file type, date, size and other possible 
criteria.
§ umask: User Mask or User file creation MASK : It is used to set the permissions for 
files/directories newly created on a Linux Machine. 
§ chmod : It will change the file or directory access permissions. 
§ chown : It will change the ownership of the file a file. Only root user can execute this.
§ chgrp : It will changes the group ownership of a file or directory. Only root user can execute 
this.
§ cp : It will copy file contents of one file to another file. 
§ mv : It will move or rename the file. 
§ file : Determine file type.
§ wc : Counts the number of lines, words, bytes, or characters in a file.
§ ln : It will create the link between files


Text Editor Commands
§ vi or vim: Text editor.
§ nano : Another Test editor



Text Reading/Display Commands
§ echo : For display purpose we will use. Like System.out.print() method in Java.
§ cat : Display the contents of a file 
§ head : Print the first 10 lines of each FILE to standard output.
§ tail : It will display the last 10 rows. 
§ more :It is a filter for paging through text one screenful at a time (stop the display on each 
screen)
§ less : less is the same except you can scroll back and forward.
§ sort: It is used to sort the output in numeric or alphabetic order .
§ tr: Translate characters
§ sed: Stream editor.
§ grep: which stands for "global regular expression print," processes text line by line and prints 
any lines which match a specified pattern



System Resources Commands
§ who : Displays the current users working on the system.
§ w : Show who is logged on and what they are doing
§ users : Displays a compact list of the users currently logged on the system. 
§ whoami : Display the current user info who gave this command
§ whereis : Path/locate the binary, source, and manual page files for a command. 
§ date : Print or set the system date and time
§ df : Report file system disk space usage
§ du : Estimate file space usage.
§ hostname : Show or set the system host name.
§ ifconfig (OR) hostname -i (OR) ip a : To find the IP address.
§ man : Display the on-line manual pages.
§ info: 
§ help: 
§ whatis: The whatis command displays a summary line from the man page for the specified 
command in Linux.
§ service : It will give the status of service.
§ systemctl list-unit-files: It will list all services.
§ uptime: Tells how long the system has been running.
§ last: show listing of last logged in users


Process Management Commands
§ ps : Display the current process running.
§ kill : Kill the process
§ top : Display Linux tasks.
§ sar: (System Activity Report): It is used to collect the CPU, Memory and I/O usage


Archive/Data Backup Commands
§ zip : Package and compress (archive) files 
§ unzip :Extract compressed files in a ZIP archive.
§ tar : It is used to archive the directory/file



User/Group Administration Commands
§ useradd : Creates a new user account. ---> Only root user can execute this command 
§ passwd : Changes a user's password
§ Note: Old password is first requested then new password is requested twice for confimation
§ chage : It is used to see user related “threshold details” such as user disable time etc. 
§ groupadd : create a new group ---> Only root user can execute this command 
§ usermod : Changes user attributes. ---> Only root user can execute this command
§ id : It is one more command which will show the user details such as his primary group and 
his secondary group. 
§ groups : Displays group membership. Means display the user belongs to which groups.
§ lid: Display user’s groups or group’s users. à Only root user can execute.
§ su : To switch user. To come out from the user press Ctrl+d, logout or exit.
§ sudo : Execute a command as another user.
§ userdel : Removes a user account. ---> Only root user can execute this command 
§ groupdel : Delete group. ---> Only root user can execute this command 



Automating/Scheduling Tasks Commands
§ Cron: Cron is a daemon that executes scheduled commands. Cron also reads /etc/crontab. 
crontab: Crontab is the program used to install, deinstall or list the tables used to drive the cron 
daemon in Vixie Cron. 
Crontab format:
# Minute Hour Day of Month Month Day of Week Command /Script
# (0-59) (0-23) (1-31) (1-12 or Jan-Dec) (0-6 or Sun-Sat) /usr/bin/find
*/1 * * * * /usr/bin/find -à Every one min, cronjob will trigger
Example:
*/1 * * * * /home/bhaskar/devops/lscmd.sh >> /home/bhaskar/lscmd.log 2>&1


Remote Access Commands
§ ssh : Secure Shell
§ scp : Secury Copy between servers.



Hardware Information Commands 
§ free: To find the amount of free and used RAM memory in the system.
§ dmidecode -t 17 : It Give the RAM information like Type of RAM(SD RAM, DRAM or 
DDR2/3), Speed, Manufacture etc --> Root user can perform this command
§ vmstat: I will gives the virtual memory statistics


Communication Commands
§ mail : Sends and receives mail.


Other Commands
§ clear : Clears the terminal screen.
§ cal : Displays a calendar
§ wget : The non-interactive network downloader.
§ tee: : It is command is used to store and view (both at the same time) the output of any other command.
§ script : This command records your login session in a typescript in the current directory.
§ ping: The ping command sends ICMP ECHO_REQUEST to network hosts.
§ telnet: 
§ history : Displays the recently executed commands .
§ uname: 
§ cat /etc/*releases
§ netstat -tunlp: 
§ watch: Using watch command we can execute the command periodically.
§ shutdown: 
§ restart: 
§ reboot: 
§ exit (OR) Ctrl +d (OR) logout :


