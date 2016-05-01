#Common Linxu Terminal Commands

------
###1. Uname 
Uname command displays important information about the system such as — Kernel name, Host name, Kernel release number, processor type, etc.,

```
$ uname -a
```

###2. Less 
Less is very efficient while viewing huge log files, as it doesn’t need to load the full file while opening.

```
$ less huge-log-file.log
One you open a file using less command, following two keys are very helpful.

CTRL+F – forward one window
CTRL+B – backward one window
```

###3. Change to TUI (text based user intface, aka commandline terminal interface) from GUI

CTRL + ALT + F1 // change from GUI to commandline terminal interface (Text Base User Interface) TUI

ALT + F7 // change from TUI to GUI

username: jun

password: space

jun@jun-ThinkPad-Edge-E540: ~$ // jun is the user/username @ hostname/machine name jun-ThinkPad-Edge-E540


###4. Whoami
```
whoami // jun

hostname //jun-ThinkPad-Edge-E540

fully qualified domain name, i.e www.duckname.com

hostname -f  // see the fully qualified domain name
```

###5. ~ or $Home
~ means $Home, every user on the Linux has a home directory under the /home directory (/home/jun, is the home for user jun)

```
cd // go back home
cd ~ // go back home
cd $HOME // go back home
echo ~
echo $HOME
```

###6. cd -
cd - // change between previous and current directroy

###7. ls
```
ls -l // long list the directory
ls -lh // long list the dir in human friendly format (size in kb/mb/gb ect)
ls -lhS // S sort by size
ls -lhSr // S sort by size, r: reserver sort order
ls -lht // sort by time, new time to old time
ls -lhtr // sort by reverse time, old to new time
ls -R // list all the directories and their sub-directories
ls -R /usr/share/doc // shows all the subdirectores and files in the direcotry
// Working with Files and Directories
```

###8. sudo su - // swap user, - flag
```
sudo su - // same as sudo su - root // change to the root user, whoami = root
sudo su - root
exit
sudo su - jun
exit
```

###9. cp
```
cp // copy files 
cp -p oldfile newfile // -p preserves the access permission of the file
cp -r old_dir new_dir // -r copy directories recursively
cp -rp old_dir new_dir
cp -a old_dir new_dir == cp -rp old_dir new_dir
cp -i old_file new_file // -i will ask if you want to copy, prompt for confirmation
cp -ip old_file new_file
cp -ia old_file new_file
```

###10. rm, mv
```
clear // clear the console
CTRL + l // clear the console
mkdir -p directory1/dir2/dir3 // -p means create parent directory if it doesn't exist

mv -i old_file new_file // -i will prompt for confirmation
rm -r testdir // -r means recursive
rm -r -i testdir // -i means interactie, will prompt for confirmation
rm -fi test.txt  // -i overrides -f, so it'll ask for confirmation
rm -if test.txt // this command -f overrides the -i, so it won't ask for confirmation, just go and del the file without hesitation

```

###11. man, aprops
```
// Search for system documentation
man rm // manual page for command rm
man -k remove // -k means keyword
man -k search 
apropos remove // apropos is same as man -k

```

###12. df (disk free), du (disk usage)
```
// Querying the disk usage
df // disc free 
df -h // disc free in human readable form

du -h . // disc usage in human readable of the current directory
du -hs .  // s means summary
du -hs /usr/share/doc // shows the human readable summary of the directory 
du -hs / // 
du -h --max-depth=1 /home/jun/ // list all the disk usage summary of 1 depth deep of directory /home/jun
du -ah // don't run it from / root dir as it'll dispaly the size of every file on the entire linux harddisk

```

###13. find, -i: ignore case, -name, -not or !, -type f: file, -type d (dir), -empty,
```
find // find locations of files/directories quickly
find -name 'myProgram.c' // find file by name
find -iname 'MyProgram.c' // -i ignore case, find file using name, ignore case

find / -name 'myProgram.rb' // find the file under all sub-dirs starting from the root dir
find / -maxdepth 2 -name 'myProgram.c' // find the file under root and 2 level down
find / -name docker -type d -xdev // search against all directories below / for docker found in directories but only on the existing file system

sudo find / -name docker -type d // better run it as root or superuser
find -maxdepth 1 -not -iname "MyCProgram.c" // inverting the match, shows the files/dirs whose name are not MyProgram.c. Since the maxdepth is 1, this will only look the current directory.
find ./test -name 'abc*' ! -name '*.php'

find ~ -empty // find all empty files in the home directory
find . -maxdepth 1 -empty
find . -maxdepth 1 -empty -not -name ".*" // List only the non-hidden empty files only in the current directory.

find . -type d // find all directories
find . -type f // find only the normal files
find . -type f -name ".*" // find all hidden files
find -type d -name ".*" //find all hidden directories

find . -exec ls -ld {} \;
find . -iname jun.txt -exec rm -i {} \; // find file jun.txt from current dir and rm it;
find . -user bob // find files belongs to user bob
find . -type f -exec ls -s {} \; | sort -n -r | head -5 // find top 5 big files
```

###14. poweroff, shutdown, reboot
```
sudo poweroff
sudo shutdown -h now // -h means halt
sudo init 0 // shut down
sudo shutdown 
sudo shutdown -r now // -r means reboot, same as sudo reboot
sudo reboot 
sudo init 6 // reboot 
```

###15.CTRL + W/U/D/R/L
Delete last word from command line
CTRL + W 

Delate current line from command line
CTRL + U

Logout current terminal
CTRL + D

Recursive search
CTRL + R

Clear screen
CTRL + L

Show command history
History

Grep command history
history | grep xxx // history | grep docker

###16. chmod: change file mode bits
####chmod: change file mode bits/change file permission. Chmod changes the file permission. There exist 3 types of permission on a file (folder or anything but to keep things simple we will be using file): read (r) = 4, write (w) = 2, execute (x) = 1. For read and write permission: 4 + 2 = 6. Now permission need to be set for 3 kinds of user and usergroup. The first is owner, then usergroup and finally world (others). 
```
$ rwxr-x--x   abc.sh // onwer: rwx, usergroup: r, x, others/world: x

$ chmod 777 abc.sh //To change its permission and provide read, write and execute permission to owner, group and world.

$ chmod 666 abc.sh // only read and write permission to all three

$ chmod 711 abc.sh // owner: rwx, usergroup: x, others: x

```

###17. chown: change file owner and group.
####Every file belongs to a group of user and a owner.
```
$ root@tecmint:~# ls -l 

$ drwxr-xr-x 3 server root 4096 May 10 11:14 Binary 
$ drwxr-xr-x 2 server server 4096 May 13 09:42 Desktop
Here the directory Binary is owned by user “server” and it belongs to usergroup “root” where as directory “Desktop” is owned by user “server” and belongs to user group “server“.

This “chown” command is used to change the file ownership and thus is useful in managing and providing file to authorised user and usergroup only.

$ root@tecmint:~# chown server:server Binary

$ drwxr-xr-x 3 server server 4096 May 10 11:14 Binary 
$ drwxr-xr-x 2 server server 4096 May 13 09:42 Desktop
Note: “chown” changes the user and group ownership of each given FILE to NEW-OWNER or to the user and group of an existing reference file.
```

###17. Create new user

###18. tar, gzip, bzip
#### Linux 'tar' stands for 'tape archive'. The tar is most widely used command to create compressed archive files and that can be moved easily from one disk to anther disk or machine to machine. -c: creates a new .tar archive file, -v: verbosely show the .tar file progress, -f: file name type of the archive file, -z: create compressed gzip archive file, -j: create highly compressed bz2 archive file, -C:path of the driectory, -t: lst content
```
$ tar -cvf juns_file.tar /home/jun/juns_files  // creates a tar archive file called juns_file.tar for a directory /home/jun/juns_files

$ tar -cvzf juns_images.tar.gz /home/junsImages  // create a compressed gzip archive file for the dir /home/junsImages in the current directory

$ tar -cvjf phpfiles.tar.bz2 /home/phpFiles // create a highly compressed tar bz2 file for a dir /home/php

tar -xvf juns_file.tar  // untar files using -x: extract
tar -xvf juns_images.tar.gz
tar -xvf phpfiles.tar.bz2 
tar -xvf thumbnails.tar.gz -C /home/public_images/thumbnails/ // -C: path of the directory
tar -tvf jun_file.tar // list the content
tar -tvf juns_images.tar.gz
tar -tvf phpfiles.tar.bz2
```

###19. Environment Variables
```
* Inspect the current PATH variables: `echo $PATH`
* Append directory to the existing PATH: `export PATH=$PATH:/path/to/binary`
* Declare a new environment variable: `export {variable}=/path/to/binary`
* Edit system-wide environment variables: `nano /etc/environment`
* Create an alias for a command: `nano ~/.bash_aliases` followed by `alias {alias name}='{command}'`
```

###20. Uptime
####Uptime command shows since how long your system is running and the number of users are currently logged in and also displays load average for 1,5 and 15 minutes intervals.

$ uptime


###21. w or who
####It will displays users currently logged in and their process along-with shows load averages. also shows the login name, tty name, remote host, login time, idle time, JCPU, PCPU, command and processes.

$ w //w command is a combination of uptime and who
$ who

###22. whoami or who am i
####whoami command print the name of current user. You can also use “who am i” command to display the current user.
$ whoami
$ who am i

###23. grep
####Grep searches for a given string in a file
$ grep jun /ect/passwd
$ grep -i jun /etc/passwd

###24. cal / cal 01 1985
####The “cal” (Calendar), it is used to displays calendar of the present month or any other month of any year that is advancing or passed.
$ cal // show current month
$ cal 01 1985 // show Jan 1985
$ cal 11 2050  // show Nov 2050


###25. date
####The “date” (Date) command print the current date and time on the standard output, and can further be set.
$ date
$ date --set='14 May 2017 13:57' // set the time for system wide change


###26. cat / concatenation
####The “cat” stands for (Concatenation). Concatenate (join) two or more plain file and/or print contents of a file on standard output. Note: “>>” and “>” are called append symbol. They are used to append the output to a file and not on standard output. “>” symbol will delete a file already existed and create a new file hence for security reason it is advised to use “>>” that will write the output without overwriting or deleting the file.

$ cat a.txt b.txt c.txt d.txt >> abcd.txt
$ cat abcd.txt








