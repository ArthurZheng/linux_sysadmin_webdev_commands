#Compiled list of commonly used Linux commands


## Basic Commands

- list all users accounts in the terminal

dscacheutil -q user | grep -A 3 -B 2 -e uid:\ 5'[0-9][0-9]'

dscl . list /Users | grep -v '^_'

- cd
    - cd -
    - cd ~
    - cd ~yadong
- ls
- pwd
- cp
- mv
- rm
- mkdir
- touch
- man
- info

## Text

- cat
- more
- less
- head
- tail
    - tail -f
- cut
- join
- sort
    - sort -s
- uniq
- paste
- tac
- tr
- sed
- awk
- grep/egrep

## FS

- ln
    - ln -s
- find
- locate
- df
- du
- ncdu
- mount/umount
- file
- stat
- rename
- strings
- hd
- tar
- gzip
- bzip2
- split
- dd

## Network

- ifconfig
- ip
- dig
- mtr
- nc

## Package Mgmt

- apt
    - apt-get
    - apt-cache
- yum
- dpkg

## Job Management

- ^z
- ^c
- jobs
- fg
- bg
- kill
- killall
- crontab

## Permission

- chown
- chgrp
- chmod


## Monitoring

- ps
- top
- htop
- free
- vmstat
- pstree
- iostat
- netstat
- dstat
- stap(systemtap)
- hdparm
- uname

## Debugging

- gdb
- strace
- ltrace
- wireshark
- tshark
- ldd
- dmesg
- /proc

## Testing

- curl


## MISC

- xargs
- parallel
- expr
- 2>&1
- > /dev/null
- tee
- lsb_release -a
- yes
- cal
- env
- export
- seq
- nl
- shuf
- perl -e
- python -m
- alias

## Session

- nohup
- disown
- screen
- w
- who
- whoami
- finger
- reset

## Shell Scripting (bash)

- subshells
```
# do something
(cd /other/folder; other command)
# continue
```
- $$

## Tips

- ^r
- ^w
- ^u
- ^l
- python -m SimpleHTTPServer
- sudo !!
- man ascii
- touch {1..10}.txt

## vim

## ssh

---

Linux System Admin Notes

1. Ping to find out he IP address 
$ ping -c 1 google.com

2. Use tail to view the content of the file in real time using tail -f. This is useful to view the log files, that keeps growing. The command can be terminated using CTRL-C.
$ tail -f log-file

3. Go to the 143rd line of file
$ vim +143 filename.txt

4. Go to the first match of the specified
$ vim +/search-term filename.txt

5. Display filesize in human readable format (e.g. KB, MB etc.,)
$ ls -lh

6. To view current running processes.
$ ps -ef | less

7. Displays the file system disk space usage. By default df -k displays output in bytes.
df -h displays output in human readable form. i.e size will be displayed in GB’s.
$ df -h

8. Use kill command to terminate a process. First get the process id using ps -ef command, then use kill -9 to kill the running Linux process as shown below. You can also use killall, pkill, xkill to terminate a unix process.

$ ps -ef | grep vim
ramesh    7243  7222  9 22:43 pts/2    00:00:00 vim

$ kill -9 7243

9. Get confirmation before removing the file.

$ rm -i filename.txt

10. Copy file1 to file2 preserving the mode, ownership and timestamp.

$ cp -p file1 file2
Copy file1 to file2. if file2 exists prompt for confirmation before overwritting it.

$ cp -i file1 file2


11. Apply the file permissions recursively to all the files in the sub-directories.
$ chmod -R ug+rwx file.txt (owner, grup, others/world)

12. Uname command displays important information about the system such as — Kernel name, Host name, Kernel release number, processor type, etc.,

$ uname -a


13. less is very efficient while viewing huge log files, as it doesn’t need to load the full file while opening.

$ less huge-log-file.log
One you open a file using less command, following two keys are very helpful.

CTRL+F – forward one window
CTRL+B – backward one window

14. To connect to a remote mysql database. This will prompt for a password.

$ mysql -u root -p -h 192.168.1.2
To connect to a local mysql database.

$ mysql -u root -p

15. Ping a remote host by sending only 5 packets.

$ ping -c 5 gmail.com

16. Find top 5 big files
# find . -type f -exec ls -s {} \; | sort -n -r | head -5

17. IOPS (Input/Output Operations Per Second, pronounced eye-ops) is a common performance measurement used to benchmark computer storage devices like hard disk drives (HDD), solid state drives (SSD), and storage area networks (SAN).

18. PEM/PPK

========================================================================================================================

Basic Linux Commands

CTRL + ALT + F1 // change from GUI to commandline terminal interface (Text Base User Interface) TUI

ALT + F17 // change from TUI to GUI

username: jun

password: space

jun@jun-ThinkPad-Edge-E540: ~$ // jun is the user/username @ hostname/machine name jun-ThinkPad-Edge-E540

whoami // jun

hostname //jun-ThinkPad-Edge-E540

fully qualified domain name, i.e www.duckname.com

hostname -f  // see the fully qualified domain name

pwd

cd ..

pwd // /home

cd ~ // every user on the Linux has a home directory under the /home directory

echo ~ // ~ means home of the user

echo $HOME

cd - // change between previous and current directory

cd // change you to home directory

cd /home/jun // change to a specific directory

// listing files and directories
touch // creates a file without any content

ls -l // long list the directory

ls -lhS // S sort by size

ls -lhSr // S sort by size, r: reserver sort order

ls -lht // sort by time, new time to old time

ls -lhtr // sort by reverse time, old to new time

ls -R // list all the directories and their sub-directories

ls -R /usr/share/doc // shows all the subdirectores and files in the direcotry

// Working with Files and Directories

cp // copy files 

sudo su - // change to the root user, whoami = root

sudo su -

exit

sudo su - jun

exit

cp -p oldfile newfile // -p preserves the access permission of the file

cp -r old_dir new_dir

cp -rp old_dir new_dir

cp -a old_dir new_dir == cp -rp old_dir new_dir

cp -i old_file new_file // -i will ask if you want to copy, prompt for confirmation

cp -ip old_file new_file

cp -ia old_file new_file

clear // clear the console

mv -i old_file new_file

mkdir -p directory1/dir2/dir3 // -p means create parent directory if it doesn't exist

rm -r testdir // -r means recursive

rm -r -i testdir // -i means interactie, will prompt for confirmation

rm -fi test.txt

rm -if test.txt // this command -f overrides the -i, so it won't ask for confirmation, just go and del the file without hesitation


// Search for system documentation

man rm // manual page for command rm

man -k remove // -k means keyword

man -k search

apropos remove // apropos is same as man -k


// Querying the disk usage

df // disc free 

df -h // disc free in human readable form

pwd

du -h . // disc usage in human readable of the current directory

du -hs .  // s means summary

du -hs /usr/share/doc // shows the human readable summary of the directory 

du -hs / // 

du -h --max-depth=1 /home/jun/ // list all the disk usage summary of 1 depth deep of directory /home/jun

========================================================================================================================
Beginner Server Administrator Commands

arp //	Command mostly used for checking existing Ethernet connectivity and IP address

ifconfig 

df // disk free, display filesystem information

df -h  

du -h . // disk usage of the current dir in human readable format

du -hs . // disk free usage summary of the current dir in human readable format

du -h --max-depth=2 /home/jun

du -a  // don't run it from the / root directroy as it'll dispaly the size of every file on the entire Linux hardisk

find // find locations of files/directories quickly

find / -name docker -type d -xdev // search against all directories below / for docker found in directories but only on the existing file system

sudo find / -name docker -type d // better run it as root or superuser

ifconfig // command line tool to configure/check all network cards/interfaces

ifconfig eth0 10.1.1.1

man ifconfig  


------

ubuntu-cheatsheet
=================

Ubuntu commands for people who don't know Linux

## System Management
* Restart the machine: `sudo shutdown -r now`

## User Management
* Create a new user: `useradd {username}`

## Disk Management
* Checking for disk space on available volumes: `df -h` command
* Check for size of folders in current working directory: `du -h --max-depth=1`

## File System
* Create .tar.gz / .tgz files: `tar -czvf {output.tgz} {folder}`
* Extract .tar.gz / .tgz files: `tar -xzvf {input.tgz} {path}`
* Create .zip files: `zip -r {output.zip} {folder}`
* Extract .zip files to directory: `unzip {input.zip} -d {folder}`
* Watch a log file real-time: `tail -f {file}`
* Find files containing text: `grep -Rl {search} {path}` or case insensitive `grep -Rli {search} {path}`
* Download a file from the internet: `wget {url}`
* Back up your stuff locally: `rsync {source} {destination}`
* Back up your stuff to another server: `rsync -avz -e ssh {path} {user}@{host}:{path}`

## File Permissions
* Make a file executable: `chmod +x {filename}`

## Environment Variables
* Inspect the current PATH variables: `echo $PATH`
* Append directory to the existing PATH: `export PATH=$PATH:/path/to/binary`
* Declare a new environment variable: `export {variable}=/path/to/binary`
* Edit system-wide environment variables: `nano /etc/environment`
* Create an alias for a command: `nano ~/.bash_aliases` followed by `alias {alias name}='{command}'`

## Process Management
* Kill a process: `kill {pid}`
* See all running processes: `ps aux`
* Get PIDs of running processes under a specific name: `ps aux | grep {name}` or `ps aux | grep {name} | awk '{print $2}'`

## Machine Properties
* Modify the host name: `sudo nano /etc/hostname`
* Set a static IP address: `sudo nano /etc/network/interfaces`
* Modify hosts: `sudo nano /etc/hosts`

## Cron Jobs
* Check existing cron jobs: `crontab -e`

## Networking
* What IP adress is assiged to me? `ifconfig`
* What TCP/IP ports are open and what programs are listening on them? `lsof -i -P` (needs to have lsof installed and be run as root)
* Where do I configure my network interfaces? `vi /etc/network/interfaces` then run `ifdown <interface>` and then `ifup <interface>`
* What are the details of a specific network interface? `iwlist <interface> scan`
* Connect to a specific wireless network for a given interface? `iwconfig <interface> essid "<ssid name>"`
* Get an IP address assigned from a router? `dhclient <interface>`
* How do I list all NAT rules? `iptables -L`
* What are all of the available network devices for this machine? `lspci`

------

------------------------------------------------
You can add any commands or improve existing one
However, you must follow the current pattern is:

# THE_LINUX_COMMAND_EXPLANATION
THE_LINUX_COMMAND_1
THE_LINUX_COMMAND_2
...
------------------------------------------------

Find relatives
==============

# find string in file
find . -name MY_FILE_PATTERN | xargs grep 'MY_STRING'
# same as above, but just with the file name
find . -name "MY_FILE_PATTERN" -exec grep -l MY_STRING {} \;
# find string in file and give, with, before each file name, the number of time the MY_STRING appears in the file
find . -name "MY_FILE_PATTERN" | xargs grep 'MY_STRING' | awk -F: '{print $1}' | uniq -c
# less on a source file with syntax highlighting (need highlight : http://www.andre-simon.de/doku/highlight/en/highlight.html)
highlight -l -A SOURCE_FILE  | less -R
# find string in specified path and file pattern
find . -ipath './MY_DIRECTORY/FOOBAR/*/*.MY_EXTENSION' | xargs grep 'MY_STRING'
# open files in editor which string match in files
gedit `find . -ipath './MY_DIRECTORY/FOOBAR/*/*.MY_EXTENSION' | xargs grep 'MY_STRING' | awk -F: '{print $1}'`
# open files in editor which string match in files
find . -ipath './MY_DIRECTORY/FOOBAR/*/*.MY_EXTENSION' -exec perl -pi -e 's/MY_ORIG_STRING/MY_REPLACED_STRING/' {} \;

# replace string in files which strings match in files
find . -ipath './merlin-data/src/*/*.xml' -exec perl -pi -e 's/http:\/\/hibernate.sourceforge.net\//http:\/\/www.hibernate.org\/dtd\//' {} \;
# Another way to replace string in files 
perl -p -i -e 's/relativePath>../relativePath>..\/../g' `find ./ -name pom.xml`

# delete files recursively
$ find . -name .DS_Store -delete

#Find all those pesky files above 20mb
find . -size +20000k -exec du -h {} \;


media relatives
===============

# erase a CDRW
sudo cdrecord blank=all -immed dev=/dev/cdrw

# mount an Iso file
mount -o loop -t iso9660 file.iso /media/iso

# extract audio from a video (without reencoding it)
ffmpeg -i mandelbrot.flv -vn -acodec copy mandelbrot.mp3

Bash relatives
=============

# Delete last word from command line
CTRL + W 

# Delate current line from command line
CTRL + U

# Logout current terminal
CTRL + D

# Recursive search
CTRL + R

# Clear screen
CTRL + L

# Show command history
History

# Grep command history
history | grep xxx // history | grep docker


# Change under ubuntu the default color of directory that is other-writable (o+w) and not sticky, see: http://www.bigsoft.co.uk/blog/index.php/2008/04/11/configuring-ls_colors
echo "OTHER_WRITABLE 01;34" > ~/.dircolors

System relatives
================

# display a desktop notification
notify-send "Title" "This is a message"

# When the system's freezed :
Keep Left Alt & Print Screen pressed, then R, S, E, I, U, B (Raising a Skinny Elephant Is Utterly Boring)

# Find broken symlinks in a specified directory
for i in `find MY_DIRECTORY -type l`; do [ -e $i ] || echo $i is broken; done

# Get BIOS version
sudo dmidecode -s bios-version

Simply commands
===============

# kill a process by its window
xkill #And squeeze the trigger

Display relatives
================

# Send display to specific output
xrandr --output HDMI1 --right-of LVDS1


------

# Show Ethernet Ports
ifconfig

# Show Ethernet Ports IP Addresses
ip addr 

# Restarting Network
# Restarting network interfaces in Ubuntu 14.04 is not as easy as it should be. 
# Due to a “feature” in Ubuntu 14.04, service network restart no longer works to restart network interfaces. 
ifconfig interfacename down 
ifconfig interfacename up

# Find out what Ethernet card is assigned to which port.  Contains lots of information such as Vendor, Product, Mac Address, etcc
lshw -class network

# Lookup DNS ip address of the domain name
host www.linux.org

# Download a file from the internet
wget http://path.to.file

# List active connections to and from system
netstat -tupl

# Location of network information
/etc/network/interfaces

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
<--- End of /etc/network/interfaces -->


## lsb_release Command To Find Out Linux Distribution Name/Version

The lsb_release command displays certain LSB (Linux Standard Base) and distribution-specific information. Type the following command:
$ lsb_release -a

Say hello to /proc/version

Type the following command to see kernel version and gcc version used to build the same:
$ cat /proc/version

How Do I Find Out My Kernel Version?

Type the following command:
$ uname -a

OR
$ uname -mrs

---
##To list all users you can use:

cut -d: -f1 /etc/passwd
To add a new user you can use:

sudo adduser new_username
or:

sudo useradd new_username
See also: What is the difference between adduser and useradd?

To remove/delete a user, first you can use:

sudo userdel username
Then you may want to delete the home directory for the deleted user account :

sudo rm -r /home/username
(Please use with caution the above command!)

To modify the username of a user:

usermod -l new_username old_username
To change the password for a user:

sudo passwd username
To change the shell for a user:

sudo chsh username
To change the details for a user (for example real name):

sudo chfn username
---

