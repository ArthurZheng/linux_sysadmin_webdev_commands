#Linux Server Admin Commands
------

###1. Ping
$ ping -c 1 google.com
$ ping -c 5 gmail.com //ping a remote host by sending only 5 packets.

###2. Tail
#### Use tail to view the content of the file in real time using tail -f. This is useful to view the log files, that keeps growing. The command can be terminated using CTRL-C.
tail -f log-file.txt // watch a log-file real-time

###3. Process Management
#### view the current running process
```
ps -ef | less
ps -ef | grep init // show init process only
ps -aux | less // see all running processes
ps aux | grep docker
ps -ef | grep ssh

ps -A | grep -i ssh 
ps - A // To list status of all the processes along with process id and PID, use option ‘-A‘.

Get PIDs of running processes under a specific name: `ps aux | grep {name}` or `ps aux | grep {name} | awk '{print $2}'`
```

###4. kill, killall, pkill, xkill to terminate a unix process with uid
#### Use kill command to terminate a process. First get the process id using ps -ef command, then use kill -9 to kill the running Linux process as shown below. You can also use killall, pkill, xkill to terminate a unix process.

```
$ ps -ef | grep vim
ramesh    7243  7222  9 22:43 pts/2    00:00:00 vim

$ kill -9 7243
```

###5. mysql
####To connect to a remote mysql database. This will prompt for a password.
$ mysql -u root -p -h 192.168.1.2 // -u: user, -p: prompt for password, -h:host

####To connect to a local mysql database.
$ mysql -u root -p

###6. ifconfig 
####command line tool to configure/check all network cards/interfaces
ifconfig

###7. ip addr
ip addr

###8. host url
```
host www.linux.org // lookup DNS address of the domain name
host -t a www.facebook.com // find out all ip address of facebook.com

whois 69.171.228.40 | grep CIDR // find CIDR for 69.171.228.40

To prevent outgoing access to www.facebook.com, enter:
$ iptables -A OUTPUT -p tcp -d 69.171.224.0/19 -j DROP

You can also use domain name, enter:
$ iptables -A OUTPUT -p tcp -d www.facebook.com -j DROP
$ iptables -A OUTPUT -p tcp -d facebook.com -j DROP

dig www.linux.org 
$ telnet www.cyberciti.biz 80 // use telnet to see if firewall allows to connect to port:80

```

###9. netstat
$ netstat -tupl // list active connections to and from system, 
$ netstat -tulpn //find out if ports are open or not
$ netstat -tulpn | grep :80 // find out if tcp port 80 open or not
#### Location of network information
/etc/network/interfaces

```
# Sample /etc/network/interfaces file content.   
<--- Start of /etc/network/interfaces -->
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

# The loopback network interface
auto lo
iface lo inet loopback

# Realtek RTL81111GR - Driver r8169 - Has more features than Intel one. 
# dhcp configuration
auto p2p1
iface p2p1 inet dhcp

# Intel I218V - Driver e1000e
# dhcp configuration
auto eth0
iface eth0 inet dhcp

# add bridge interface
# bridge off p2p1
iface br0 inet dhcp
bridge_ports p2p1
bridge_stp off
auto br0

# add bridge interface 2
# bridge off eth0
iface br1 inet dhcp
bridge_ports eth0
bridge_stp off
auto br1
```

###10. Find out what Ethernet card is assigned to which port. Contains lots of information such as Vendor, Product, Mac Address, etcc
lshw -class network


###11. Networking 
####Restarting network interfaces in Ubuntu 14.04 is not as easy as it should be. Due to a “feature” in Ubuntu 14.04, service network restart no longer works to restart network interfaces. 
```
$ ifconfig interfacename down 
$ ifconfig interfacename up

$ ifconfig // what IP address is assigned to me
$ lsof -i -P (needs to have lsof installed and be run as root) //What TCP/IP ports are open and what programs are listening on them

vim  /etc/network/interfaces` then run `ifdown <interface>` and then `ifup <interface>` // config network interfaces

$ iwlist <interface> scan // the details of a specific network interface

$ iwconfig <interface> essid "<ssid name>" // Connect to a specific wireless network for a given interface
$ dhclient <interface> // Get an IP address assigned from a router
$ sudo iptables -L // list all NAT rules
lspci // list the available network devices for this machine
```

### iptables
#### Displaying the status of your firewall
$ iptables -L -n -v // -L: List rules, -v: Display detailed info, -n: display IP addr and port in numeric format
$ iptables -L -n -v --line-numbers

####To display INPUT or OUTPUT chain rules, enter:
$ iptables -L INPUT -n -v
$ iptables -L OUTPUT -n -v --line-numbers

#### Stop/Start/Restart the Firewall
$ service iptables stop
$ service iptables start
$ service iptables restart




###12. Machine Properties
```
* Modify the host name: `vim /etc/hostname`
* Set a static IP address: `vim /etc/network/interfaces`
* Modify hosts: `vim nano /etc/hosts`

```

###13. Cron Jobs
#### Schedule and run tasks in the background automatically at regular intervals using crontab command. Cron is a daemon to run schedule tasks. Cron wakes up every minute and checks schedule tasks in the crontable. Crontab (Cron TABle) is a table where you can schedule such kind of repeated tasks.
```
crontab -l //check existing cron jobs
crontab -u jun -l // list cron jobs of user jun -u: means user, -l: list
crontab -e // edit existing cron jobs
crontab -i -r // -i: prompt for confirmation, -r: remove // remove complete scheduled jobs and ask for confirmation

System administrator can use predefine cron directory as shown below.

/etc/cron.d
/etc/cron.daily
/etc/cron.hourly
/etc/cron.monthly
/etc/cron.weekly
Below scheduled job to delete empty files and directory from /tmp at 12:30 am daily as user root
30 0 * * *   root   find /tmp -type f -empty -delete
30 0 * * *   root   find /tmp -type f -empty -delete >/dev/logs 2>&1 // redirect all the output under /dev/logs instead of send email to user account executing cronjob by default.


```

###14. netstat 
####netstat command displays various network related information such as network connections, routing tables, interface statistics, masquerade connections, multicast memberships etc..,
```
$ netstat -a // list all network ports
$ netstat -at // list all TCP prots
$ netstat -s // show statistics for all ports
```

###15. nslookup
####A network utility program used to obtain information about Internet servers. As its name suggests, the utility finds name server information for domains by querying DNS.

$ nslookup google.com
$ nslookup -query=mx google.com // query mail exchange record
$ nslookup -type=ns google.com // query name server
$ nslookup -type=any google.com // query DNS record
$ nslookup -type=soa google.com // query start of authority

###16. dg
####dig is a tool for querying DNS nameservers for information about host addresses, mail exchanges, nameservers, and related information. This tool can be used from any Linux (Unix) or Macintosh OS X operating system. The most typical use of dig is to simply query a single host.

dig google.com
dig google.com +nocomments // turn off comment lines

###17. mysqldump
####mysqldump commands dumps (backups) all or a particular database data into a given a file
$ mysqldump -u root -p --all-databases > /home/server/Desktop/backupfile.sql



