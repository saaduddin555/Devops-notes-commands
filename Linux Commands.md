# Linux commands

# Basic File Operation Commands
date        (it tells date of linux system)
cal         (calender it shows)
whoami      (It will show username of the linux and type)
w           (it shows complete details of User Information)
id          (gets all uid and gid information)
pwd         (present working follder/Directory)
cd          (change directory)
cd ..       (Change to previous directory)
cd /        (change to root directory)
mkdir       (mkdir means create of make the directory)
ls          (list of files or folders)
ls -al      (gives detailed information about files and folders)
touch       (It helps to create a file)
nano        (It is a editor where we can edit the file same as note pad)
             Eg: nano linux basics.txt ,It will create a files as well as it will open the editor mode, to do changes in that file
                 ctrl+x= To exit
                 ctrl+s= To Save
                 ctrl+k= To cut the Text
                 ctrl+u=to paste the text
                 alt+u+undo
                 alt+e=Redo
                 ctrl+g=Get help
                 ctrl+\=Replace
                 when u press ctrl+s it asks u to reconfirm "save modified buffer" press "Y" to save and press "N" to reject
                 Ctrl+c to cancel the changes and go back

cat             (To read or open a file in terminal mode)  Eg: cat linux basics.txt
mv              (To rename a file)   Eg: mv linux basics.txt linux.txt
rm              (To delete a file)   Eg: rm linux basics.txt
rmdir           (To remove a Folder) Eg: rm linuxfolder
cp              (To copy the file or folder to other destination) Eg: cp linux.txt linux
history         (Gets all history of commands used in terminal)
mv              (To move a file mv is used) Eg: mv just.txt linux/
tree            (Tree command is used to get proper visualization of the folder structure)
                sudo apt install tree = To install tree package
ls-al           (TTo see all the hidden files)
ls -a           (Just Just hidden files) 
ls -F           (Shows Folder symbolically)
ls -it          (count of items in folder)
ls -lt          (List out last modifed and properties of files and folders)
ls -lh          (file size info)
ls -lR          (To see all folders and sub directories Information)
tac             (To print out results of file in reverse manner same as cat command but shows result in reverse mode)
head            (read only gead section of file)  Eg: head python.txt
head -2         (Reads only two lines of file)    Eg: head -2 pyhton.txt
tail            (Reads bottom Information of the file)
tail -3         (Reads botoom 3 lines of the file)
alias           (To change or modify the command name sometimes to shorten a command like p=pwd) Eg:alias p="pwd" or alias c="cat"  cmd:c python.txt it opens the file.
ls > output.txt (The output of that ls command is stored in form of text file and not shown in Terminal)
pwd > output.txt (Gets the output in file of present working directory)
pwd >> otput.txt (To add all output and not erase the earlier putput and add the new content below or previous value)
locate           (TO locate a file or search) 
apt              (advance packaging tool)
sudo             (root user)                   Eg: sudo apt install mlocate  :To insatll locate package
tar 
pv 
chmod 
grep 
diff 
sed 
ar 
man 
pushd 
popd 
fsck 
testdisk 
seq 
fd 
pandoc 
$PATH 
awk 
join 
jq 
fold 
uniq 
journalctl 
tail 
stat 
fstab 
echo 
less 
chgrp 
chown 
rev 
look 
strings 
type 
rename 
mount 
umount 
install 
fdisk 
mkfs 
rsync 
df gpg 
vi 
nano 
du 
ln 
patch 
convert 
rclone 
shred 
srm
systemctl

# Storage/Ram/Disk

top             (Gets process info cpu, memory, utilization, root, all configuration details)
du -sh *                 (Storage Information) and * represents all storage information
du -sh python.txt        (Shows disk info a file or folder)
du -sh .[!.]**           (To View all hidden files) (. Before a folder or file represents Hidden file)
du -sch .[!.]**          (TO View hidden files as well as normal files and folders)
df -h                    (TO view Complete disk space)
mp stat                  (Gets Process info statistically) sudo spt install sysstat
mp stat 2                (Gets Process info every 2 seconds)
vmstat                   (Memory/Ram usage info)
acpi                     (Battery Information)
iostat                   (Input/output data live read write metrics)
ls cpu                   (gets all cpu information)
ls hw                    (gets all harware information)
ls usb                   (To see all usb info if mounted)
free                     (To check ram memory usage/free/shared/available)
uname -a 

# User and Account Commands

sudo -s or sudo -i          (To convert to root user)
id                         (gets all uid and gid information)
w                          (it shows complete details of User Information)
who                        (Gets all user info)
whoami                     (To check users and accounts in os)
useradd                    Eg: sudo useradd syed (To add a user called as syed)
su uername                 (To switch user Eg: su syed : to switch to syed accout and enter password)
userdel                    (To delete a user Eg: sudo userdel syed )
last                       (To get all Activities of user login details and status of the user)
shutdown                   (To shut down the user of the PC  Eg: sudo shutdown)
exit                       to exit from that place)
logout                     (To logout out of that user)
.........................................................................................................................................................................
# Networking Commands

# 1 netstat
netstat                     

The netstat command lets you discover which sockets are connected and which sockets are listening. Meaning, it tells you which ports are in use and which processes are using them. It can show you routing tables and statistics about your network interfaces and multicast connections.

Listing All Sockets        (netstat -a | less)
The -a (all) option makes netstat show all the connected and waiting sockets. This command is liable to produce a long listing, so we pipe it into less.

The listing includes TCP (IP), TCP6 (IPv6), and UDP sockets.

The “Active Internet” section lists the connected external connections and local sockets listening for remote connection requests. That is, it lists the network connections that are (or will be) established to external devices.

The “UNIX domain” section lists the connected and listening internal connections. In other words, it lists the connections that have been established within your computer between different applications, processes, and elements of the operating system.

The “Active Internet” columns are:

Proto: The protocol used by this socket (for example, TCP or UDP).
Recv-Q: The receive queue. These are incoming bytes that have been received and are buffered, waiting for the local process that is using this connection to read and consume them.
Send-Q: The send queue. This shows the bytes that are ready to be sent from the send queue.
Local address: The address details of the local end of the connection. The default is for netstat to show the local hostname for the address, and the name of the service for the port.
Foreign address: The address and port number of the remote end of the connection.
State: The state of the local socket. For UDP sockets, this is usually blank. See the state table, below.
For TCP connections, the state value can be one of the following :

LISTEN: Server-side only. The socket is waiting for a connection request.
SYN-SENT: Client-side only. This socket has made a connection request and is waiting to see if it will be accepted.
SYN-RECEIVED: Server-side only. This socket is waiting for a connection acknowledgment after accepting a connection request.
ESTABLISHED: Server and clients. A working connection has been established between the server and the client, allowing data to be transferred between the two.
FIN-WAIT-1: Server and clients. This socket is waiting for a connection termination request from the remote socket, or for an acknowledgment of a connection termination request that was previously sent from this socket.
FIN-WAIT-2: Server and clients. This socket is waiting for a connection termination request from the remote socket.
CLOSE-WAIT: Server and client. This socket is waiting for a connection termination request from the local user.
CLOSING: Server and clients. This socket is waiting for a connection termination request acknowledgment from the remote socket.
LAST-ACK: Server and client. This socket is waiting for an acknowledgment of the connection termination request it sent to the remote socket.
TIME-WAIT: Server and clients. This socket sent an acknowledgment to the remote socket to let it know that it received the remote socket’s termination request. It is now waiting to make sure that acknowledgment was received.
CLOSED: There is no connection, so the socket has been terminated.

The “Unix domain” columns are:

Proto: The protocol used by this socket. It will be “unix.”
RefCnt: Reference count. The number of attached processes connected to this socket.
Flags: This is usually set to ACC , which represents SO_ACCEPTON, meaning the socket is waiting for a connection request. SO_WAITDATA, shown as W, means there is data waiting to be read. SO_NOSPACE, shown as N, means there is no space to write data to the socket (i.e., the send buffer is full).
Type: The socket type. See the type table below.
State: The state of the socket. See the state table below.
I-Node: The file system inode associated with this socket.
Path: The file system path to the socket.

The Unix domain socket type can be one of the following:

DGRAM: The socket is being used in datagram mode, using messages of fixed length. Datagrams are neither guaranteed to be reliable, sequenced, nor unduplicated.
STREAM: This socket is a stream socket. This is the commonplace “normal” type of socket connection. These sockets are designed to provide reliable sequenced (in-order) delivery of packets.
RAW: This socket is being used as a raw socket. Raw sockets operate at the network level of the OSI Model and don’t reference TCP and UDP headers from the transport level.
RDM: This socket is located on one end of a reliably delivered messages connection.
SEQPACKET: This socket is operating as a sequential packet socket, which is another means of providing reliable, sequenced, and unduplicated packet delivery.
PACKET: Raw interface access socket. Packet sockets are used to receive or send raw packets at the device driver (i.e., data link layer) level of the OSI model.
The Unix domain socket state can be one of the following:

FREE: This socket is unallocated.
LISTENING: This socket is listening for incoming connection requests.
CONNECTING: This socket is in the process of connecting.
CONNECTED: A connection has been established, and the socket is able to receive and transmit data.
DISCONNECTING: The connection is in the process of being terminated.

Listing Sockets by Type
The netstat -a command can provide more information than you need to see. If you only want or need to see the TCP sockets, you can use the -t (TCP) option to restrict the display to only show TCP sockets.

netstat -at | less                (The display out is greatly reduced. The few sockets that are listed are all TCP sockets.)

The -u (UDP) and -x (UNIX) options behave in a similar way, restricting the results to the type of socket specified on the command line. Here’s the -u (UDP) option in use:

netstat -au | less

Only UDP sockets are listed.

Listing Sockets by State

To see the sockets that are in the listening or waiting state, use the -l (listening) option.

netstat -l | less

The sockets that are listed are those that are in the listening state.

This can be combined with the -t (TCP, -u (UDP) and -x (UNIX) options to further home in on the sockets of interest. Let’s look for listening TCP sockets:

netstat -lt | less

Now, we see only TCP listening sockets.


Network Statistics by Protocol:

To see statistics for a protocol, use the -s (statistics) option and pass in the -t (TCP), -u (UDP), or -x (UNIX) options. If you just use the -s (statistics) option on its own, you’ll see statistics for all protocols. Let’s check the statistics for the TCP protocol.

netstat -st | less

A collection of statistics for the TCP connections is displayed in less.

Showing Process Names and PIDs
It can be useful to see the process ID (PID) of the process using a socket, together with the name of that process. The -p (program) option does just that. Let’s see what the PIDs and process names are for the processes using a TCP socket that is in the listening state. We use sudo to make sure we receive all of the information that is available, including any information that would normally require root permissions.

sudo netstat -p -at

We’ve got an extra column called “PID/program name.” This column lists the PID and name of the process using each of the sockets.

Listing Numeric Addresses

Another step we can take to remove some ambiguity is to display the local and remote addresses as IP addresses instead of their resolved domain and hostnames. If we use the -n (numeric) option, the IPv4 addresses are shown in dotted-decimal format:

sudo netstat -an | less

The IP addresses are shown as numeric values. The port numbers are also shown, separated by a colon ” : ” from the IP Address.

An IP address of 127.0.0.1 shows that the socket is bound to the loopback address of the local computer. You can think of an IP address of 0.0.0.0 as meaning the “default route” for local addresses, and “any IP address” for foreign addresses. IPv6 addresses shown as “::” are also all zero addresses.

The ports that are listed can be easily checked to see what their usual purpose is:

22: This is the Secure Shell (SSH) listening port.
25: This the Simple Mail Transfer Protocol (SMTP) listening port.
53: This is the Domain Name System (DNS) listening port.
68: This is the Dynamic Host Configuration Protocol (DHCP) listening port.
631: This is the Common UNIX Printing System (CUPS) listening port.

Displaying the Routing Table

The -r (route) option displays the kernel routing table.

sudo netstat -r

And, here’s what the columns mean:

Destination: The destination network or destination host device (if the destination is not a network).
Gateway: The gateway address. An asterisk “*” appears here if a gateway address is not set.
Genmask: The subnet mask for the route.
Flags: See the flags table, below.
MSS: Default Maximum Segment Size for TCP connections over this route—this is the largest amount of data that can be received in one TCP segment.
Window: The default window size for TCP connections over this route, indicating the number of packets that can be transferred and received before the receiving buffer is full. In practice, the packets are consumed by the receiving application.
irtt: The Initial Round Trip Time. This value is referenced by the kernel to make dynamic adjustments to TCP parameters for remote connections that are slow to respond.
Iface: The network interface from which the packets sent over this route are transmitted.
The flags value can be one of:

U: The route is up.
H: Target is a host and the only destination possible on this route.
G: Use the gateway.
R: Reinstate the route for dynamic routing.
D: Dynamically installed by the routing daemon.
M: Modified by the routing daemon when it received an Internet Control Message Protocol (ICMP) packet.
A: Installed by addrconf, the automated DNS and DHCP config file generator.
C: Cache entry.
!: Reject route.
Finding the Port Used by a Process
If we pipe the output of netstat through grep, we can search for a process by name and identify the port it is using. We use the -a (all), -n (numeric) and -p (program) options used previously, and search for “sshd.”

sudo netstat -anp | grep "sshd"

grep finds the target string, and we see that the sshd daemon is using port 22.

Of course, we can also do this in reverse. If we search for “:22”, we can find out which process is using that port, if any.

sudo netstat -anp | grep ":22"

This time grep finds the “:22” target string, and we see that the process using this port is the sshd daemon, process ID 751.

List the Network Interfaces
The -i (interfaces) option will display a table of the network interfaces that netstat can discover.

sudo netstat -i

This is what the columns mean:

Iface: The name of the interface. The enp0s3 interface is the network interface to the outside world, and the lo interface is the loopback interface. The loopback interface enables processes to intercommunicate within the computer using networking protocols, even if the computer is not connected to a network.
MTU: The Maximum Transmission Unit (MTU). This is the largest “packet” that can be sent. It consists of a header containing routing and protocol flags, and other metadata, plus the data that is actually being transported.
RX-OK: The number of packets received, with no errors.
RX-ERR: The number of packets received, with errors. We want this to be as low as possible.
RX-DRP: The number of packets dropped (i.e., lost). We also want this to be as low as possible.
RX-OVR: Number of packets lost due to overflows when receiving. This usually means that the receiving buffer was full and could not accept any more data, but more data was received and had to be discarded. The lower this figure, the better, and zero is perfect.
TX-OK: The number of packets transmitted, with no errors.
RX-ERR: The number of packets transmitted, with errors. We want this to be zero.
RX-DRP: The number of packets dropped when transmitting. Ideally, this should be zero.
RX-OVR: The number of packets lost due to overflows when transmitting. This usually means the send buffer was full and could not accept any more data, but more data was was ready to be transmitted and had to be discarded.
Flg: Flags. See the flags table below.
The flags represent the following:

B: A broadcast address is in use.
L: This interface is a loopback device.
M: All packets are being received (i.e., in promiscuous mode). Nothing is filtered or discarded.
O: Address Resolution Protocol (ARP) is turned off for this interface.
P: This is a Point-to-Point (PPP) connection.
R: The interface is running.
U: The interface is up.

List Multicast Group Memberships

Simply put, a multicast transmission enables a packet to be sent only once, regardless of the number of recipients. For services such as video streaming, for example, this increases the efficiency from the sender’s point of view by a tremendous amount.

sudo netstat -g

The columns are quite simple:

Interface: The name of the interface over which the socket is transmitting.
RefCnt: The reference count, which is the number of processes attached to the socket.
Group: The name or identifier of the multicast group.
The New Kids on the Block
The route, ip, ifconfig, and ss commands can provide a lot of what netstat is capable of showing you. They’re all great commands and worth checking out.

We’ve focused on netstat because it is universally available, regardless of which Unix-like operating system you’re working on, even the obscure ones.
                                                          
To Know More use https://www.howtogeek.com/657780/how-to-use-the-traceroute-command-on-linux
.......................................................................................................................................................................

# Other networking commands:

Trace route

ifconfig                                                (Gets all Network related Info)

Ping

ip

ss

whois

fail2ban

bmon

dig

finger

nmap

ftp

curl

wget

iptables

ssh-keygen

ufw

# Process Commands

alias 

screen

top 

nice 

renice

progress 

strace 

systemd 

tmux 

chsh 

history 

at 

batch 

free 

which 

dmesg 

chfn 

usermod 

ps 

chroot 

xargs 

tty 

pinky 

lsof 

vmstat 

timeout 

wall 

yes 

kill 

sleep 

sudo 

su 

time 

groupadd 

usermod 

groups 

lshw 

shutdown 

reboot 

halt 

poweroff 

passwd 

lscpu 

crontab 

date 

bg 

fg
........................................................................................................................................................................

# File Compression

# 1
Compress an Entire Directory or a Single File
Use the following command to compress an entire directory or a single file on Linux. It’ll also compress every other directory inside a directory you specify–in other words, it works recursively.

tar -czvf name-of-archive.tar.gz /path/to/directory-or-file
Here’s what those switches actually mean:

-c: Create an archive.
-z: Compress the archive with gzip.
-v: Display progress in the terminal while creating the archive, also known as “verbose” mode. The v is always optional in these commands, but it’s helpful.
-f: Allows you to specify the filename of the archive.
Let’s say you have a directory named “stuff” in the current directory and you want to save it to a file named archive.tar.gz. You’d run the following command:

tar -czvf archive.tar.gz stuff
Or, let’s say there’s a directory at /usr/local/something on the current system and you want to compress it to a file named archive.tar.gz. You’d run the following command:

tar -czvf archive.tar.gz /usr/local/something

# 2
Compress Multiple Directories or Files at Once

While tar is frequently used to compress a single directory, you could also use it to compress multiple directories, multiple individual files, or both. Just provide a list of files or directories instead of a single one. For example, let’s say you want to compress the /home/ubuntu/Downloads directory, the /usr/local/stuff directory, and the /home/ubuntu/Documents/notes.txt file. You’d just run the following command:

tar -czvf archive.tar.gz /home/ubuntu/Downloads /usr/local/stuff /home/ubuntu/Documents/notes.txt

# 3

Exclude Directories and Files
In some cases, you may wish to compress an entire directory, but not include certain files and directories. You can do so by appending an --exclude switch for each directory or file you want to exclude.

For example, let’s say you want to compress /home/ubuntu, but you don’t want to compress the /home/ubuntu/Downloads and /home/ubuntu/.cache directories. Here’s how you’d do it:

tar -czvf archive.tar.gz /home/ubuntu --exclude=/home/ubuntu/Downloads --exclude=/home/ubuntu/.cache

The --exclude switch is very powerful. It doesn’t take names of directories and files–it actually accepts patterns. There’s a lot more you can do with it. For example, you could archive an entire directory and exclude all .mp4 files with the following command:

tar -czvf archive.tar.gz /home/ubuntu --exclude=*.mp4

# 4

Use bzip2 Compression Instead
While gzip compression is most frequently used to create .tar.gz or .tgz files, tar also supports bzip2 compression. This allows you to create bzip2-compressed files, often named .tar.bz2, .tar.bz, or .tbz files. To do so, just replace the -z for gzip in the commands here with a -j for bzip2.

Gzip is faster, but it generally compresses a bit less, so you get a somewhat larger file. Bzip2 is slower, but it compresses a bit more, so you get a somewhat smaller file. Gzip is also more common, with some stripped-down Linux systems including gzip support by default, but not bzip2 support. In general, though, gzip and bzip2 are practically the same thing and both will work similarly.

For example, instead of the first example we provided for compressing the stuff directory, you’d run the following command:

tar -cjvf archive.tar.bz2 stuff

# 5
Extract an Archive
Once you have an archive, you can extract it with the tar command. The following command will extract the contents of archive.tar.gz to the current directory.

tar -xzvf archive.tar.gz

It’s the same as the archive creation command we used above, except the -x switch replaces the -c switch. This specifies you want to extract an archive instead of create one.

You may want to extract the contents of the archive to a specific directory. You can do so by appending the -C switch to the end of the command. For example, the following command will extract the contents of the archive.tar.gz file to the /tmp directory.

tar -xzvf archive.tar.gz -C /tmp

If the file is a bzip2-compressed file, replace the “z” in the above commands with a “j”.


This is the simplest possible usage of the tar command. The command includes a large number of additional options, so we can’t possibly list them all here. For more information. run the info tar command at the shell to view the tar command’s detailed information page. Press the q key to quit the information page when you’re done. 

# 6 
To Zip and make an Archive
Zip python.zip python  (To make a python folder into a zip)

Unzip python.zip       (It unzips all converted folders)


.......................................................................................................................................................................
# File Permissions:
                    File Permissions is a concept where we give permissions to the groups, users, admin, root. In all of these the access is given to partially or fully controlled depends up on role to role.
    In Permissions the access are like read, write and excecute. where the individual person or user are given such permissions to perform.
    I linux there are file permissions which are given to folder/file.
     ls-al to view all files and hidden files and there permissions also 

Structure of folder permission= drwxrwxr-x The directory file permission starts with letter "d" and indicates it is a folder.

Structure of file permission= -rw-rw-r-- A normal file doesnt have "d" before of its permissions, and indicates as file.

Permission denied error= It denies access to that particular file or folder in which a user need to fix the permissions to excecute read/write

This is why permissions is given

d-rwx-rwx-r-x=  (d(directory)-rwx(user)-rwx(Group)-r-x(Others)) The - symbol between r-x indicates there is no write permission given and need to give if required.

r=read, w=write, x=excecute d=indicate property that it is folder/directory

the - between rwx-rwx-rwx means seperation of users, group, other and fully permission given for all

when the x excecutable permission is not given to file, those files or shell file commands wont excecute, hence give permissions before u execute any commands.

Example of commands to set for user, group and others:

-rw-rw-r-- for user no x(excecution is given), for group no x(excecution is given) for others no w and x(write and exceution is given to fix it)

chmod +x practice.sh         (To give permission of execution to Everyone) here +x means to add -x means to remove)

chmod g+x practice.sh        (To give permissions to group or g-x means to remove permissions to group)

chmod u+x practice.sh        (To give permissions to user and u-x means to remove permissions to user)

chmod o+x practice.sh        (To give permissions to others and o-x means to remove permissions to others)

Instead of x we can give read r or write w in the place of x

Advanced Concept in permission:

Give permissions by number

r=4, w=2, x=1

r=read w=write x=excecute

hence 

000=(User,group,others) when u give permission u need to add which is required and place eg: read and write of others is chmod 006 filename.sh (read=4+write=2 i.e 6)

chmod 000 practice.sh (000 means no permission for read, write and excecute for all)

chmod 700 practice.sh (700 means all permission for read, write and excecute is given only for user)

chmod 770 practice.sh (770 means all permission for read, write and excecute for users and group)

chmod 110 practice.sh (110 means no permission given for read, write "Only Exceute given for user and group" and for Others No for all as 0)

chmod 444 practice.sh (444 means permission for read only, for user,group,other and write and excecute denied for all)

chmod 756 practice.sh (756 means all permission for read, write and excecute for user, read and Excecute for group and read and write for others)

chmod 777 practice.sh (777 means all permission for read, write and excecute for all)


Above all are examples and can place accordingly
......................................................................................................................................................................

# To run a Script
sudo apt bash name-of-script-to-run.sh          (To run a bash script)


......................................................................................................................................................................
# Notes about Root Directory and FOlders and usage of File it contents

/ — The Root Directory
Everything on your Linux system is located under the / directory, known as the root directory. You can think of the / directory as being similar to the C:\ directory on Windows — but this isn’t strictly true, as Linux doesn’t have drive letters. While another partition would be located at D:\ on Windows, this other partition would appear in another folder under / on Linux.

/bin — Essential User Binaries
The /bin directory contains the essential user binaries (programs) that must be present when the system is mounted in single-user mode. Applications such as Firefox are stored in /usr/bin, while important system programs and utilities such as the bash shell are located in /bin. The /usr directory may be stored on another partition — placing these files in the /bin directory ensures the system will have these important utilities even if no other file systems are mounted. The /sbin directory is similar — it contains essential system administration binaries.

/boot — Static Boot Files
The /boot directory contains the files needed to boot the system — for example, the GRUB boot loader’s files and your Linux kernels are stored here. The boot loader’s configuration files aren’t located here, though — they’re in /etc with the other configuration files.

/cdrom — Historical Mount Point for CD-ROMs
The /cdrom directory isn’t part of the FHS standard, but you’ll still find it on Ubuntu and other operating systems. It’s a temporary location for CD-ROMs inserted in the system. However, the standard location for temporary media is inside the /media directory.

/dev — Device Files
Linux exposes devices as files, and the /dev directory contains a number of special files that represent devices. These are not actual files as we know them, but they appear as files — for example, /dev/sda represents the first SATA drive in the system. If you wanted to partition it, you could start a partition editor and tell it to edit /dev/sda.
This directory also contains pseudo-devices, which are virtual devices that don’t actually correspond to hardware. For example, /dev/random produces random numbers. /dev/null is a special device that produces no output and automatically discards all input — when you pipe the output of a command to /dev/null, you discard it.

/etc — Configuration Files
The /etc directory contains configuration files, which can generally be edited by hand in a text editor. Note that the /etc/ directory contains system-wide configuration files — user-specific configuration files are located in each user’s home directory.

/home — Home Folders
The /home directory contains a home folder for each user. For example, if your user name is bob, you have a home folder located at /home/bob. This home folder contains the user’s data files and user-specific configuration files. Each user only has write access to their own home folder and must obtain elevated permissions (become the root user) to modify other files on the system.

/lib — Essential Shared Libraries
The /lib directory contains libraries needed by the essential binaries in the /bin and /sbin folder. Libraries needed by the binaries in the /usr/bin folder are located in /usr/lib.

/lost+found — Recovered Files
Each Linux file system has a lost+found directory. If the file system crashes, a file system check will be performed at next boot. Any corrupted files found will be placed in the lost+found directory, so you can attempt to recover as much data as possible.

/media — Removable Media
The /media directory contains subdirectories where removable media devices inserted into the computer are mounted. For example, when you insert a CD into your Linux system, a directory will automatically be created inside the /media directory. You can access the contents of the CD inside this directory.

/mnt — Temporary Mount Points
Historically speaking, the /mnt directory is where system administrators mounted temporary file systems while using them. For example, if you’re mounting a Windows partition to perform some file recovery operations, you might mount it at /mnt/windows. However, you can mount other file systems anywhere on the system.

/opt — Optional Packages
The /opt directory contains subdirectories for optional software packages. It’s commonly used by proprietary software that doesn’t obey the standard file system hierarchy — for example, a proprietary program might dump its files in /opt/application when you install it.

/proc — Kernel & Process Files
The /proc directory similar to the /dev directory because it doesn’t contain standard files. It contains special files that represent system and process information.

/root — Root Home Directory
The /root directory is the home directory of the root user. Instead of being located at /home/root, it’s located at /root. This is distinct from /, which is the system root directory.

/run — Application State Files
The /run directory is fairly new, and gives applications a standard place to store transient files they require like sockets and process IDs. These files can’t be stored in /tmp because files in /tmp may be deleted.

/sbin — System Administration Binaries
The /sbin directory is similar to the /bin directory. It contains essential binaries that are generally intended to be run by the root user for system administration.

/selinux — SELinux Virtual File System
If your Linux distribution uses SELinux for security (Fedora and Red Hat, for example), the /selinux directory contains special files used by SELinux. It’s similar to /proc. Ubuntu doesn’t use SELinux, so the presence of this folder on Ubuntu appears to be a bug.

/srv — Service Data
The /srv directory contains “data for services provided by the system.” If you were using the Apache HTTP server to serve a website, you’d likely store your website’s files in a directory inside the /srv directory.

/tmp — Temporary Files
Applications store temporary files in the /tmp directory. These files are generally deleted whenever your system is restarted and may be deleted at any time by utilities such as tmpwatch.

/usr — User Binaries & Read-Only Data
The /usr directory contains applications and files used by users, as opposed to applications and files used by the system. For example, non-essential applications are located inside the /usr/bin directory instead of the /bin directory and non-essential system administration binaries are located in the /usr/sbin directory instead of the /sbin directory. Libraries for each are located inside the /usr/lib directory. The /usr directory also contains other directories — for example, architecture-independent files like graphics are located in /usr/share.The /usr/local directory is where locally compiled applications install to by default — this prevents them from mucking up the rest of the system.

/var — Variable Data Files
The /var directory is the writable counterpart to the /usr directory, which must be read-only in normal operation. Log files and everything else that would normally be written to /usr during normal operation are written to the /var directory. For example, you’ll find log files in /var/log.
........................................................................................................................................................................
# Other Commands 



