---
title: "Linux Training"
date: 2019-05-11T21:38:49-07:00
draft: true
---

# Linux Bootcamp
+ ssh -p 2022 jordan@obscurty

+ ssh nsl@linuxclass-005.nullpro.be
+ NullSp4c3Lab5

exit  
quit  
CTRL C  
CTRL D

---
names | x | x
---|---|---|
Natalie | Joseph | Data
Lance | Miguel | x


---
## Command Line Arguments

$ `ls -l -a /etc`  
$ `ls -t` (list in order of time)  
$ `echo "Hello World`  
$ `scho -n`  
$ `/` root  
$ `echo $HOME`  `/home/nsl`  
$ `w`  who
$ `mkdir one/two -p` -p mkmakes a parent directory  
$ `cat demo_file.txt` look inside a file    
$ `less nasa_19950801.tsv` use (access logs from nasa)  
### using less to search 
$ `less nasa_19950801.tsv` 
once you are in less...   
 /searchterm
+ n - next result
+ N - previous result
+ h - for more help
/hella/-i
+ add \c to your search for case insensitive  
### Head & Tail
$ `head nasa_19950801.tsv 10` or any number you want   
$ `tail nasa_19950801.tsv 10`  
follow a log file  
$ `tail -f nasa_19950801.tsv` CTRL C  
### Tab completion
press tab twice for all matches
### GNU RegEx aka GREP
already know what file you have but you want to search it  
$ `grep hella nasa_19950801.tsv`  
#### $ `grep -r hella *`  
$ `grep -R hella *`  (follows symbolic links) 
$ `grep -ir hella *`  (-i -r )(case insensitive)  
### PWD
print working directory
$ `pwd`  
### CD change directory
cd is an aspect of the shell - ir's a shell command
$ `cd filename`  
$ `cd ..`  
$ `cd` takes you home  
$ `cd /` takes you home then $ `cd`    
### which
$ `which ls` >> `/bin/ls`  
$ `which man` `/usr/bin/man`
### Copy files - cp
$ `cp nasa_19950801.tsv nasa_hella.tsv`  
$ `cp nasa_19950801.tsv logs/` copy this into the logs dir  
$ `cp nasa_19950801.tsv logs/nasa_hella-cool.tsv`  

A path with a `/` in frobt of it it is an absolute path and it goes to the root of the system
like `/logs`  

### Move && Rename Files with `mv`
$ `mv nasa_19950801.tsv logs/`  
$ `mv logs/nasa_19950801.tsv logs/nasa-is-nice.tsv`  

### Remove with `rm`
$ `rm`  
$ `rmdir directory-name`  
$ `rmdir -rf directory-name`  
$ `rm -i` adds a prompt

### Touch
will create a file, if it already exists touch will update the UTC time stamp
$ `touch filename`  
$ `touch test`  
$ `ll` >> `0 May  4 19:48 test`
$ `date` >>  `Sat May  4 19:50:56 UTC 2019`   
$ `touch test`  >> `0 May  4 19:51 test`   
### Editing text files using nano
$ `nano demo_text.txt`
  GNU nano 2.5.3         File: demo_file.txt  
  CTRL == ^  
  
  
  nano | x | x
  ---|---|---
  ^G | Get Help |
  ^X | Exit | 
  ^O | Write | save without exiting
  ^R | Read File |
  ^W | Where us | 
  ^\ | Replace | 
  ^K | cut text |
  ^ U | Uncut text 
  ^J | justify |
  ^T | to spell
  ^M | line break

:set list
  
  2 chars that make a newline  
  1. 
  
#### Line break styles
+ https://palantir.github.io/tslint/rules/linebreak-style/
+ https://en.wikipedia.org/wiki/Newline

exiting vim - https://www.amazon.com/How-Exit-Vim-Chris-Worfolk-ebook/dp/B01N5M1U6W

### Find
swiss army knife of searches finding things  
find  [-H]  [-L]  [-P]  [-D debugopts] [-Olevel] [starting-
       point...] [expression]  
`find` locates the files you are looking for  
`grep` searched

$ `find . test` (`.` - current directory)  
$ `find . -name "demo"`  
$ `find . -name "*.log"`  
$ `find /home/msl -name syslog.log`  
$ `find . -empty`  
$ `find . -atime 90`
$ `man find`  
$ `find /var/log/ -readable`  
$ `find /var/log -name "*.log"`  
$ `find -type f -mtime -1` (fine file modified in last day)  
if you don't give it a path it will search your current directory  
$ `find ~ -name "*.log"`  
$ `find $HOME -name "*.log"` 

### Comparing files with diff
< == first file  
> == second file

+ colordiff
+ wdiff  
+ vimdiff  

$ `diff demo_file.txt demo_file_v2.txt`   
```
1c1
< Editing shdfjkhTHIS LINE IS THE 1ST UPPER CASE LINE IN THIS FILE.
---
> THIS LINE IS THE 1ST UPPER CASE LINE IN THIS FILE.
5c5
< Two lines above this line is empty.
---
> The line above this line is empty.
nsl@linuxclass-005:~$ 
```
`1c1` above shows what line and char the diff is on and at  

$ `diff demo`  

###Linux file permissions
Bit on or off  
user froup others  
read write execute  

ls -l will show the permissions  
drwxrwxr-x 2  
-rw-r--r-- 1  
`-` plain file  
`d` directory
`rwx` if not set it is a dash `-`  
|user|

| filetype | user | user | user | group | group | group | other | other | other |
|---|---|---|---|---|---|---|---|---|---|
| d | - | r | w | x | r | w | - | r | w |

### Change file owner
chown changes the owner of a file  

`chown [desired-owner] file` (don't write in the brackets [] )  
using an `*` is called globbing  
can be recursively with -R  
chown nsl:nsl  
$ `cat /etc/passwd`   
`bin/false` - user that doesn't get to log in  
```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
messagebus:x:107:111::/var/run/dbus:/bin/false
uuidd:x:108:112::/run/uuidd:/bin/false
dnsmasq:x:109:65534:dnsmasq,,,:/var/lib/misc:/bin/false
sshd:x:110:65534::/var/run/sshd:/usr/sbin/nologin
pollinate:x:111:1::/var/cache/pollinate:/bin/false
ubuntu:x:1000:1000:Ubuntu:/home/ubuntu:/bin/bash
nsl:x:1001:1001:,,,:/home/nsl:/bin/bash
```

mac handles users and groups differently  
there is a user called sound

https://explainshell.com
don't run a web server as root because if it gets exploited then the user is just admin ot 
$ `ls -l /dev/xen/`

$ `chown nsl echo.sh`
`-rw------- 1 nsl  nsl        54 May  4 00:54 echo.sh`
`-rw------- 1 nsl  nsl        54 May  4 00:54 echo.sh`

### Change group

$ `chgrp nsl *`  

## Change file permissions with chmod
chmod  - change file mode bits

+ basic form ``  
+ Target = [u]  

cp /etc/sysctl.conf /home/nsl
-rw------- 1 nsl  nsl       248 May  4 20:05 demo_file.txt
-rw-rw---- 1 nsl  nsl       248 May  4 20:05 demo_file.txt
Change the group permissions  
$ `chmod g+rw demo_file.txt` 
Take the permissions away  
$ `chmod g-rw demo_file.txt 
every member has a group  
every file has a group associated with it  
$ `groups` >> nsl admin  
set up group `usermod` >>> ?  `man usermod`   
$ `cat /etc/group`  
```
root:x:0:
daemon:x:1:
bin:x:2:
sys:x:3:
adm:x:4:syslog,ubuntu
tty:x:5:
disk:x:6:
lp:x:7:
mail:x:8:
news:x:9:
uucp:x:10:
man:x:12:
proxy:x:13:
kmem:x:15:
dialout:x:20:ubuntu
fax:x:21:
voice:x:22:
cdrom:x:24:ubuntu
floppy:x:25:ubuntu
tape:x:26:
sudo:x:27:ubuntu
audio:x:29:ubuntu
dip:x:30:ubuntu
www-data:x:33:
backup:x:34:
operator:x:37:
list:x:38:
irc:x:39:
src:x:40:
gnats:x:41:
shadow:x:42:
utmp:x:43:
video:x:44:ubu
```
### apropo 
search the manual page names and descriptions  
+ to the purpose
+ when you know you want to do but not sure what to use
+ should be followed with a review


$ `apropos network`  

### Manuel pages
man - online reference  manuals  
https://linux.die.net/man  
+ There are 9 sections
    + 1 executable programs
    + 
uses less as its pager   
+ up 
+ down 
+ space bar page

$ `apropos passwd`  
```
chgpasswd (8)        - update group passwords in batch mode
chpasswd (8)         - update passwords in batch mode
gpasswd (1)          - administer /etc/group and /etc/gshadow
grub-mkpasswd-pbkdf2 (1) - generate hashed password for GRUB
pam_localuser (8)    - require users to be listed in /etc/passwd
passwd (1)           - change user password
passwd (1ssl)        - compute password hashes
passwd (5)           - the password file
update-passwd (8)    - safely update /etc/passwd, /etc/shadow an...
```
$ `man 5 passwd`  
$ `man sudoers`  
$ `man man`  
```
       The  table  below  shows the section numbers of the manual
       followed by the types of pages they contain.

       1   Executable programs or shell commands
       2   System calls (functions provided by the kernel)
       3   Library calls (functions within program libraries)
       4   Special files (usually found in /dev)
       5   File formats and conventions eg /etc/passwd
       6   Games
       7   Miscellaneous (including macro  packages  and  conven‐
           tions), e.g. man(7), groff(7)
       8   System administration commands (usually only for root)
       9   Kernel routines [Non standard]
```

### Sudo super/supervised user
change or become super user

 
$ `sudo less /var/log/syslog`  
$ `sudo vim /etc/sudoers`  
$ `sudo service ntp stop`   
$ `sudo -i` (changes you to root user)  

$ `echo ~` >> `~/root`  
$ `whoami` >> `root`  
`-rw-rw---- 1 nsl  nsl       248 May  4 20:05 demo_file.txt 
$ `chown root:root demo_file.txt` 
`-rw-rw---- 1 root root      248 May  4 20:05 demo_file.txt`
$ `sudo chmod o+rw demo_file.txt`  
`-rw-rw-rw- 1 root root      248 May  4 20:05 demo_file.txt`

### Software Management
+ dpkg
+ 
+
+ 
### apt
$ `sudo apt install nginx`  
$ `sudo apt remove nginx`  
$ `curl systemctl stop nginx` 
$ `sudo apt update`
$ `sudo apt upgrade`

### curl

$ `curl linuxclass-005`  
```
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

$ `curl nginx -t`  
```
curl: option -t: requires parameter
curl: try 'curl --help' or 'curl --manual' for more information
```
# 2
https://docs.google.com/presentation/d/1wTbUj5XpUeaIL2kjU8WfdUx92M7ze2VfjO-0YhWsqI0/edit#slide=id.p

ugo  
754  
7 all three  
rwx rwx rwx  
binary 421 421  
enabled 111 101   
result  

r = 4  
w = 2   
x = 1  

777 rwx rwx rwx  
440 r-- r-- ---  
400 r--------  
660 rw-rw----  
732 rwx-wx--w-  
  
- | Character | Files | Directories
---|---|---|---
Read | - | Cannot read | Contents cannot be shown
r | Can read | Contents can be shown
Write | - | Cannot write | Contents cannot be modified
w | Can write | Contents can be modified (create new files or folders; rename or delete existing files or folders); requires the execute permission
Execute | - |
Cannot execute | Cannot be accessed with cd
x | Can execute (like a program or script) | Can be accessed with cd; this is the only permission bit that in practice can be considered to be "inherited" from the ancestor directories, in fact if any folder in the path does not have the x bit set, the final file or folder cannot be accessed either, regardless of its permissions.

### Perform admin actions with sudo
`sudo less /var/log/syslog`  
`sudo vim /etc/sudoers`  
`sudo service ntp stop`  
`sudo -i`  

`ls -a`

### Symbolic Links  
`ln -s source_file target_link`  
>>  lrwxr-xr-x 1 jendiamond 999337765 7 May 11 10:32 link -> test.sh  

#### The sym link is a ponter to the file  
makes relative links so if you move either one they will break

#### To make an absolute path:  
`$PWD/testfile.txt crocodile`

`find . -name testfile.txt`

`$PWD` - environment variable for current directory  
`pwd`/testfile.txt crocodile (use backticks - graveyards)

### Public Key Authorization

+ Private Key - ~/.ssh/id_rsa  
+ Public Key - ~/.ssh/id_rsa.pub  

Use public key to get in  

### Generate the Keypair
Generate a secire keypair on your laptop  
Private keys are PRIVATE and will not work if permission are not set to 600!!(read and write for user only)  
$ `ssh-keygen -b 4096`  
`ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCVrOJ/jR3Ooga3Rong59QNNEXhh6yg8UZrj97ka28+FTXi8YkcrL/48KCG0M9Qtl8M8bx+HMuFlX5o5bAZQlBipFtDDmJrfPj1/wb4U/xMhGceoeq0EsEk3OUtr8FzYEAZObAyAT3Hhh+GCAO3Un5TPGltcz7DZg7VV7+snerAgImKsHJMmQoCmV67bESveOSo2WOTWy6QKMXawXniziJ3btS353xeJDSrZtwXS9beQqLf02NqWBYRvMtbhYYS7Iwd5BrGnPEfduUZ6nHtViFxvr08hiHRNsPMc1QeloOVeMxzhCn/NxQy2ValCv1BflKtxTEt/qDvBEgHJ6oBWifH jendiamond@sandinista`

me-4  

### SCP 
`scp` - secure copy  

securely copy your ssh key into the server  
1. $ `scp ~/.ssh/id_rsa.pub nsl@linuxclass-004.nullpro.be:~/`

Be sure it is in there   
$ ssh nsl@linuxclass-004.nullpro.be:~/  
 Look for the file `~/.ssh/id_rsa.pub`   
 exit
$ `vim .ssh/known_hosts`

#### PSWD - NullSp4c3Lab5

$ `cat `.ssh/authorized_keys`  this is a file on the server - it list of authorized public keys

$ `vim .ssh/known_hosts`  - once you connect it adds your servers fingerprint to the list of known hosts

#### Then you can log in without entering a password  
$ `ssh nsl@linuxclass-004.nullpro.be`

Disable PasswordAuthentication
PasswordAuthentication no  

$ `sudo vim /etc/ssh/sshd_config`  
pswd: NullSp4c3Lab5

Find the line:  
PasswordAuthentication yes   
Restart the system to load  
$ `sudo systemctl restart sshd`  

### Manage Users
Check the man pages for these utilities!  
Note: many of these will only work under sudo/root  
+ useradd - create users on the system (also see adduser)
+ userdel - delete users from the system
+ usermod - modify users on the system
+ passwd - set user password
+ whoami - questions your existence (prints username)

To see all the Users on a system look here but DO NOT EDIT them  
The users file (but don’t edit it): /etc/passwd

$ `less etc/password`

### Group membership
collections of Users  
Check the man pages for these utilities!  
Note: many of these will only work under sudo/root
+ groupadd - add groups to the system
+ groupdel - delete groups from the system
+ groupmod - modify groups on the system
+ groups - prints the groups that you belong to
The groups file (but don’t edit it): /etc/group

---

### Project 2: Support the Dev Team
You just started a new company and hired two developers, Jen and Jackie.   
We want to give them access to this server to run their code and check the logs.  

+ Create a group called “devteam”
+ Create users for marc and brandon, and add them to group “devteam”
+ Create a directory for their software in /opt/nsl
    + User: root
    + Group: devteam
+ Create a directory for their logs in /var/log/nsl
    + User: root
    + Group: devteam

---

We want to make sure they can edit files in the code directory and read files in the logs directory.


cat /etc/group
+ Create a group called “devteam”
    + `cat /etc/group`
+ Create users for marc and brandon, and add them to group “devteam”
    + `sudo useradd -g users -G wheel,developers jen`
+ Create a directory for their software in /opt/nsl
    + User: root
    + Group: devteam
+ Create a directory for their logs in /var/log/nsl
    + User: root
    + Group: devteam


How to Create a New User and Assign Groups in One Command
The following useradd command will create a new user named nathan with primary group users and secondary groups wheel and developers.

sudo useradd -g users -G wheel,developers nathan


chgrp [desired group] file/s

sudo chgrp www /etc/

Create group dec
$ `sudo groupadd devteam`  
Check that it is created  
$ `sudo vim /etc/ssh/sshd_config`  
###Create Users  
$ `sudo useradd jen`  
$ `sudo useradd jackie`  
### Add them to the group
$ `sudo usermod -aG devteam jen`  
$ `sudo usermod -aG devteam jackie`   
#### Check
$ `tail -n5 cat /etc/group`  


$ `ls -ld /var/log/nsl`   
ls: cannot access '/var/log/nsl': No such file or directory   
$ `sudo ls -ld /var/log/nsl`   
ls: cannot access '/var/log/nsl': No such file or directory   
$ `mkdir /var/log/nsl`   
mkdir: cannot create directory ‘/var/log/nsl’: Permission denied   
$ `sudo mkdir /var/log/nsl   
$ `sudo ls -ld /var/log/nsl`   
drwxr-xr-x 2 root root 4096 May 11 19:40 /var/log/nsl   
$ `sudo chown root:devteam /var/log/nsl`   
$ `sudo ls -ld /var/log/nsl`   
drwxr-xr-x 2 root devteam 4096 May 11 19:40 /var/log/nsl   

   
```
devteam:x:1002:jen,jackie
jen:x:1003:
jackie:x:1004:
```
### 
$ `sudo mkdir /opt/nsl`  
$ `ls -ld /opt/msl`  
$ `sudo chgrp devteam /opt/nsl`  

---

### Input/Output

Standard streams:
stdin - The input stream where data is sent to, and read by a program
Examples: keyboard, file, pipe


stdout - The output stream to the terminal and displayed on the screen
Examples: cat, echo, literally everything


stderr - Similar to stdout, but reserved for error messaging
Example: ls non_existent_file

### Input/Output Redirection

command > filename  send stdout to a file, overwrites


command >> filename send stdout to a file, appends


command < filename  send a file into a program


command1 | command2 send stdout from one program to the stdin of another program

### I/O Examples

echo "hello" | stdin “hello” passed into echo, which prints to stdout



$ `cat < output.txt`  
$ `ps aux | grep bash
`  
$ `ls >> lars.txt` 

### I/O Examples

echo "hello" | stdin “hello” passed into echo, which prints to stdout
---|---
echo < file.txt | file.txt used as stdin for echo
ps aux | grep dockeroutput from ps aux used as stdin for grep
ls > output.txt | output from ls used as stdin for file output.txt, overwrites
ls >> output.txt | output from ls used as stdin for file output.txt, appends



### alias
$ `alias`
```
alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'
alias egrep='egrep --color=auto'
alias fgrep='fgrep --color=auto'
alias grep='grep --color=auto'
alias l='ls -CF'
alias la='ls -A'
alias ll='ls -alF'
alias ls='ls --color=auto'
   
$ `alias egrep='egrep --color=auto'`  

$ vim ~/.bashrc 
$ ps aux | grep bash >> lars.txt 
$ vim ~/.bashrc 
$ which passwd
/usr/bin/passwd
$ which ls
/bin/ls
 echo $HOME
/home/lars
$ echo $USER
lars
$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
$ `echo $PSI`  

$ echo $PS1  
\[\e]0;\u@\h: \w\a\]${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$
$ `echo $EDITOR`  
$ `$EDITOR=vim`  
$ `which vim`  
/usr/bin/vim

$ `echo $LANG`  
$ env  
```
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
MAIL=/var/mail/lars
PWD=/home/lars
LANG=en_US.UTF-8
HOME=/home/lars
SHLVL=2
LOGNAME=lars
SSH_CONNECTION=24.205.141.166 10435 172.31.17.15 22
XDG_DATA_DIRS=/usr/local/share:/usr/share:/var/lib/snapd/desktop
LESSOPEN=| /usr/bin/lesspipe %s
XDG_RUNTIME_DIR=/run/user/1001
LESSCLOSE=/usr/bin/lesspipe %s %s
OLDPWD=/home/nsl
_=/usr/bin/env
```

$ `echo $PATH`
>> `/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games`

Addonmg new directories to PATH
$ export PATH=$PATH:home/nsl/scripts

bash built in 

How the Shell interprets commands

+ reads the command
checks for aliases 
checks for builtins
+ execute your command
+ copy encironment varuabkes and cinnand kune arge to process
spaen a process
 choose wjhat to rub it through ug Pythib Badh ececytabke
 check file type

### Scripting


$ bash jenscript.sh
make an executable script  
chmod u+x jenscript.sh
$ `./jenscript.sh`  

---

$ `jenscript.sh   
jenscript.sh: command not found  
$ `pwd  
/home/lars/script  
$ `export PATH=$PATH:/home/lars/scripts  
$ `jenscript.sh   
jenscript.sh: command not found  
$ `export PATH=$PATH:/home/lars/script  
$ `jenscript.sh   
total 4  
-rwxrw-r-- 1 lars lars 6 May 11 20:57 jenscript.sh  

---

```
echo Enter your name: 
read INPUT
echo Your name is $INPUT
```

#!/bin/bash - shebang  
-n - new line  
-gt - greater than symbol  
-ne equal

```
#!/bin/bash
echo -n "Enter your age: "
read AGE
if [[ "$AGE" -gt 20 ]]
then
  echo "YOU CAN DRINK"
else
  echo "YOU ARE TOO YOUNG TO DRINK"
fi
```

chmod u+x jen.script  
chmod 755 jen.script

#!/bin/bash - shebang 
tells bash what program to run the script in

### commandline parameters  

### Return Codes
get the exit code for the previous command  
$ `echo $?`  
```
   Exit status:
       0      if OK,

       1      if minor problems (e.g., cannot access subdirectory),

       2      if serious trouble (e.g., cannot access command-line argument).
```

```
#!/bin/bash
echo "This script is named $0"
echo -n "Enter your age, $1: "
read AGE
if [[ "$AGE" -gt 20 ]]
then
  echo "YOU CAN DRINK"
  RC=0
else
  echo "YOU ARE TOO YOUNG TO DRINK"
  RC=1
fi
echo "exiting with RC: $RC"
exit $RC
```

```
#!/bin/bash
ls -l backup.tar.gz
if [[ $? -ne 0 ]]
then
  echo "WARNING"
  echo "ALERTING THE OPS TEAM"
  exit 1
fi
```
$ `jenscript.sh`
```
ls: cannot access 'backup.tar.gz': No such file or directory
WARNING
ALERTING THE OPS TEAM
```

$ `touch backup.tar.gz`
```
lars@linuxclass-004:~/script$ jenscript.sh 
-rw-rw-r-- 1 lars lars 0 May 11 21:51 backup.tar.gz
```

### TLDP Conditionals
+ http://tldp.org/LDP/Bash-Beginners-Guide/html/chap_07.html
+ http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_07_01.html
+ https://books.google.com/books?id=vdZWBQAAQBAJ&pg=PA790&lpg=PA790&dq=TLDP+Conditionals&source=bl&ots=TYtIY0OpfP&sig=ACfU3U0kt-DdKovyDJlobfvrgfpbT46bxg&hl=en&sa=X&ved=2ahUKEwjdiZmYu5TiAhWHhlQKHSDXCsQQ6AEwDnoECAkQAQ#v=onepage&q=TLDP%20Conditionals&f=false

If file doesn't exist...   
```
#!/bin/bash
ls -l backup.tar.gz
if [[ ! -a -ne 0 ]]
then
  echo "WARNING"
  echo "ALERTING THE OPS TEAM"
  exit 1
fi
```

```
#!/bin/bash
ls -l backup22.tar.gz || echo "FAIL"
```



$ ``  
$ ``  
$ ``  
$ ``  
$ ``  
$ ``  
$ ``  
$ ``  
$ ``  
$ ``  
$ ``  
$ ``  
$ ``  
$ ``  
$ ``  
$ ``  
$ ``  
$ ``  
$ ``  
$ ``  
$ ``  
