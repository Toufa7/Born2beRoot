# Password Policy

> reject_username 

Check whether the name of the user in straight or reversed form is contained in the new password. If it is found the new password is rejected 

> Minlen 

minimum password length 

> Difok 

the minimum number of characters that must be different from the old password 

> Lcredit 

maximum number of lowercase characters that will generate a credit  

> Ucredit 

maximum number of uppercase characters that will generate a credit  

> Dcredit 

maximum number of digits that will generate a credi 

 

**************************************** 

# monitoring.sh

For the script “At every 10th minute” 

<https://crontab.guru/#*/10_*_*_*_*>

Don’t forget to name it <monitoring.sh>


	#!/bin/bash

	wall "

	$echo #Architecture: `uname -a`

	$echo #CPU physical : `lscpu | sed -n '5 p' | awk '{print $2}'`

	$echo #vCPU: `cat /proc/cpuinfo | grep processor | wc -l`

	$(free -m | awk FNR==2'{printf(" #Memory Usage: %d/%dMB (%.2f%%)\n", $3, $2, $3/$2 * 100)}')

	$(df -h | awk '$NF=="/"{printf " #Disk Usage: %d/%dGB (%s)\n", $3,$2,$5}')

	$echo #Last boot:`who -b | awk '{print $3,$4}'`

	$echo #LVM use: `lsblk | grep lvm | awk '{if ($1) {print "yes";exit;} else {print "no"}}'`

	$echo #Connexions TCP : `netstat -ant | grep :4242 | awk '{print $6}' | sort | uniq -c | sort -n | awk FNR==1'{print $1,$2}'`

	$echo #User log: `who | wc -l`

	$echo #Network: IP `hostname -I | awk '{print $1}' `$echo (`ip a | grep ether | awk '{print $2}'`$echo)

	$echo #Sudo : `journalctl _COMM=sudo | grep COMMAND | wc -l`$echo cmd
	"
**************************************** 

# Defense Questions

 <code><b>What’s Virtual Machine? </b> </code>


A program on computer that work like separate computer inside the main computer, in the same time also it’s isolated from the rest of the system. 

 <code><b>How a virtual machine works? </b> </code>


First, we got to define what’s a Hypervisor; 

A piece of software that runs on top of hardware that creates a virtualization platform, this software is the one who create virtual machines and responsible for isolating the VN resources from the system hardware and making the necessary implementation so that the VM can use resources 

 1) The Hypervisor manages the hardware system and separate the physical resources from the virtual environment  

 2) When a user from a VM do a task that requires additional resources from physical environment the Hypervisor manages the request so that the guest OS could access to the resources of the physical environment 

 

Their choice of operating system? 

 <code><b>The basic differences between CentOS and Debian ?</b> </code>
 
<img src="https://cdn.educba.com/academy/wp-content/uploads/2018/09/CentOS-vs-Debian-1.jpg" width="512"/>


  <code><b>The purpose of virtual machines? </b> </code>
  
  ✅ Run applications and more than one OS (each of this OS will behave as if they were hosted on a physical device)
  
  ✅ Isolated environment for developing (protection from failure)
  
  ✅ Cost saving
 

  <code><b>Since I chose Debian: the difference between aptitude and apt, and what APPArmor is?</b> </code>

<code><i>Aptitude</i></code> is front-end to advanced packaging tool which adds a user interface to the functionality thus allowing a user to interactively search for a package and install or remove it.

<code><i>Apt or Advanced Packaging Tool?</i> </code> is a free and open source software which gracefully handles software installation and removal. Initially it was designed for Debian’s .deb packages but it has been made compatible with RPM Package Manager.
 
- both apt-get and aptitude are command line package management , The most obvious difference is that aptitude provides a terminal menu interface whereas apt-get does not.

- Aptitude has a better package management than apt-get, why ?! let's see ..

Application : Try to install a simple program i'll go with a simple text editor 

> Let’s install it with apt-get:

	sudo apt-get install geany
	
<img src="https://i.ibb.co/qykkNPk/Screen-Shot-2022-02-09-at-10-59-03-AM.png" width="1024"/>

> Now let’s uninstall it:

	sudo apt-get remove geany
	
<img src="https://i.ibb.co/r68t2fW/Screen-Shot-2022-02-09-at-11-06-36-AM.png" width="1024"/>

Bad, bad…it just uninstalls geany not its dependencies (and it should because not any other package is using them). apt-get shows if you want to remove the dependencies with the ‘autotoremove’ option, which I’m sure nobody knows about it.

> Now it’s aptitude’s turn:

	sudo aptitude install geany

<img src="https://i.ibb.co/syFq0tX/Screen-Shot-2022-02-09-at-11-12-49-AM.png" width="1024"/>

> Now let’s uninstall it:

	sudo aptitude remove geany

<img src="https://i.ibb.co/Vxp3YZz/Screen-Shot-2022-02-09-at-11-15-17-AM.png" width="1024"/>

I’s evident which is more efficient: :sassy_man: aptitude 

What we get at the end? Which one is better, and which one should you use? In simple terms, you can use any of them — considering that your requirement is met.


<code><i>APPArmor</i></code> protects the operating system and applications from external or internal threats, AppArmor is a Mandatory Access Control framework. When enabled, AppArmor confines programs according to a set of rules that specify what files a given program can access. This proactive approach helps protect the system against both known and unknown vulnerabilities


  <code><b>The advantages of this password policy? And the advantages and disadvantages of its implementation? </b> </code>



Well, the main object is to enforce to use a strong and unique password that harder to crack (it protects against a range of attacks) also by using this policy we granted a higher protection of personnel valuable information, and their disadvantages that by using a strong password well make it hard to remember  

<code><b>How LVM (Logical Volume Manager) works and what it is all about? </b> </code>




With LVM we have more flexibility (dynamic partitions) when it comes to managing (create, delete, resize) 


<code><b>What’s UFW (Uncomplicated Firewall) and the value of using it? </b> </code>

briefly ; UFW it's a tool a program provide us with an interface to modify the firewall by simplyfing the configuration of firewall traffic (the amount for data being passed through a netwrok) and for a firewall it's simply a network security wall that monitors and filtere (allow ,deny outgoing and incoming data)


A firewall interface configuration tool that runs on top of iptables (is a user space utility program that allows set up and maintain a system administrator to configure the IP (Internet Protocol used to identify machines connected to a network) packet filter rules), a tool that is geared to simplifying the process of configuring a Firewall traffic (the amount of data moving across a network at a given point of time). 

UFW a software application responsible for ensuring that the system administrator can manage iptables in a simple way since it’s difficult to work with iptables, UFW provides us with an interface to modify the firewall of our device (net-filter), once we have UFW installed we can choose which ports we want to allows connections, and which ports we want to close, this will also be very useful with SSH (security communication between devices) 

UFW is an interface to iptables that is geared towards simplifying the process of configuring a firewall. While iptables is a solid and flexible tool, it can be difficult for beginners to learn how to use it to properly configure a firewall. If you’re looking to get started securing your network, and you’re not sure which tool to use, UFW may be the right choice for you. 

Firewall = a network security device that monitors and filters incoming / outgoing network traffic based on an organization's previously established security policies, A firewall only welcomes those incoming connections that it has been configured to accept (allow, block). 

 <code><b>What’s SSH (Secure Shell) and the value of using it? </b> </code>

briefly ; SSH network protocle (number of rules that controling the exchange of information easy and secure) that allows one computer to connect over a network , SSH encrypt the packets data between computers without worrying about hacking,

A network protocol (a sets of rules governing exchange of information in an easy reliable and secure way) that allows one computer to securely connect to another computer over a network (Internet), SSH encrypt automatically the packet data between computers without worrying about hacking. 

SSH makes network connection between computers with strong guarantees that the parties of the connection genius, 

 <code><b>The Mechanism of Working?</b> </code>


| User Key      | Session Key   | Host key 	  | Server Key 	  |
| ------------- | ------------- | --------    | --------	  |

A strong end to end encryption, the end-to-end encryption based on random keys that are securely negotiated for that session and then destroyed when the session over 

 <code><b>What’s Cron? </b> </code>



A system process that will automatically perform tasks (each task has defined through a single line) as per the specific schedule, a set of commands that are used for running regular scheduling tasks, run small and quick commands on scheduled basics, this is an example; 

 * * * * * SCRIPT / COMMAND   

 Day of the week (0,7)
 
 Month of year (1,12)
 
 Day of month (1,31)
 
 Hours (0,23)
 
 Minute (0,59)
 

**************************************** 

# Defense Commands


Check The Differences ; 

	Diff <file1> <file2> 

Check that the UFW; 

	systemctl status UFW 

or 

	ufw status 

Check that the SSH; 

	service ssh status 

Operating system; 

	uname –v
	
or

	neofetch (to install it $ apt-get install neofetch)

Check that the user belongs to user42 and sudo; 

	groups <username> 

Password policy 

	vi /etc/pam.d/common-password 

And 

	vi etc/login.defs 

or 

	chage -l user 

Create a new user; 

	adduser <name> 

for case with no password for a user 

	useradd <name> 

Check if the user creates or not; 

	cat /etc/passwd | cut –d: -f1 

Create a new group; 

	addgroup <name> 

Assign the new user to the new group 

	usermod –aG <group> <name> 

Check assignment; 

	getent group <name> 

Check the hostname 

	hostname 

Modify the hostname; 

	vi /etc/hostname 

view the partitions for this virtual machine 

	lsblk 

Check that the "sudo" is installed; 

	dpkg -l | grep sudo 

assigning the new user to the "sudo" group; 

	usermod –aG <name> sudo 

Checking; 

	getent group sudo 

Verifying a file in the directory indicated in the subject; 

	cat /var/log/sudo/sudo.log 

Run a simple command with sudo; 

	sudo whoami 

Check that the "ufw" is installed; 

	apt-cache policy ufw 

Check that ufw is working properly; 

	ufw status 

List all active rules in UFW; 

	ufw status 

Adding a new port; 

	ufw allow <port> 

Deleting a port; 

	1) ufw status numbered  

	2) ufw delete <number indicated at the left > 

Check that the SSH is installed; 

	dpkg -l | grep ssh 

Check that it is working properly; 

service ssh status 

Verifying that the SSH using only 4242 ports; 

	service ssh status | grep 4242 

	or 

	netstat -plant | grep 4242 

	or 

	vi /etc/ssh/ssh_config 

**************************************** 

Use ’;’    

No matter the first command cmd1 run successfully or not, always run the second command cmd2: 

Use && 

Only when the first command cmd1 run successfully, run the second command cmd2: 

Use || 

Only when the first command cmd1 failed to run, run the second command cmd2: 

 

 

 

 

**************************************** 

# Resources
 
apt vs aptitude

https://lgallardo.com/2009/03/23/apt-vs-aptitude/


How to set password policy on Linux 

https://www.xmodulo.com/set-password-policy-linux.html 

https://support.huaweicloud.com/intl/en-us/ae-ad-1-usermanual-hss/usermanual-hss.pdf 

https://www.linuxtechi.com/enforce-password-policies-linux-ubuntu-centos/ 

What is APT and Aptitude? and What’s real Difference Between Them?

https://www.tecmint.com/difference-between-apt-and-aptitude/ 

How To Set Up a Firewall with UFW 

https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-18-04 

5 Steps to Enable SSH on Debian

https://phoenixnap.com/kb/how-to-enable-ssh-on-debian 

Linux Find Out Last System Reboot Time and Date Command 

https://www.cyberciti.biz/tips/linux-last-reboot-time-and-date-find-out.html 

Check the Number of active connections on port x ? 

https://serverfault.com/questions/421310/check-the-number-of-active-connections-on-port-80 



 
