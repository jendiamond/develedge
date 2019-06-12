---
title: "Linux Training"
date: 2019-05-11T21:38:49-07:00
draft: true
---

# Linux Bootcamp

---

## Slides
+ [Class 1](https://docs.google.com/presentation/d/1OhqZri29bW76JwOS-VSb8byTHakAg5IsY-LgYoqzWJY/edit#slide=id.p)
+ [Class 2](https://docs.google.com/presentation/d/1wTbUj5XpUeaIL2kjU8WfdUx92M7ze2VfjO-0YhWsqI0/edit#slide=id.g59f52a440f_0_6)
+ [Class 3](https://docs.google.com/presentation/d/1OhqZri29bW76JwOS-VSb8byTHakAg5IsY-LgYoqzWJY)

+ https://bit.ly/nsl-linux-301  
+ https://bit.ly/nsl-linux-302  
+ https://bit.ly/nsl-linux-303  
+ NullSp4c3Lab5  
ssh nsl@linuxclass-007.nullpro.be

---

exit  
quit  
CTRL C  
CTRL D

---
names | x | x
---|---|---|
Joseph - Null Space - Instructor| Data - Null Space - Layer One | Natalie - Cal State - GIS
Lance - chatty guy - film- camera| Miguel - highschool | Dave - editor -Pietown
Miranda - neon yellow hair | Don - gray hair - sat next to me | Natalie

---

https://gohugo.io/hosting-and-deployment/hosting-on-github/

+ ssh -p 2022 jordan@obscurty
+ ssh nsl@linuxclass-005.nullpro.be
+ NullSp4c3Lab5

---

# [Class 3](https://docs.google.com/presentation/d/1OhqZri29bW76JwOS-VSb8byTHakAg5IsY-LgYoqzWJY)
<details><summary><ul><li>Advanced shell scripting</li>
  <li>Advanced terminal usage</li>
  <li>Special filesystems</li>
  <li>Monitoring the system</li>
  <li>...and more!</li></ul></summary>
https://docs.google.com/presentation/d/1OhqZri29bW76JwOS-VSb8byTHakAg5IsY-LgYoqzWJY/edit#slide=id.p

### Filesystem hierarchy

`/` - the “root” of it all.  Every file and directory resides under here  
`/home` - User’s personal directory i.e. /home/sandra  
`/root` - The root user’s home directory  
`/bin` - binaries, aka programs you can run  
`/sbin` - system binaries, administrative commands, usually requiring sudo  
`/usr` - “user” applications, also has its own /usr/bin /usr/sbin subdirectories  
`/etc` - system-wide configuration files for services and software  
`/tmp` - temporary files, often wiped between reboots  
`/lib` - system-wide libraries  
`/opt` - applications installed outside your system’s package management  
`/dev` - device files - interact with real or virtualized hardware  
`/boot` - Linux kernel images for booting the system  
`/var` - files that software writes to during operation, i.e. logs, database files

download file you want to use
wget name of file http:''

$ `echo $PATH >> /home/nsl/bin:/home/nsl/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
`
$ `mkdir bin`  
$ `mv consul bin/`

## Locate
Finding files with locate  
`locate <filename>`  
Searches a local database instead of a live search like find  
Must be manually updated with updatedb  
(find is a live search)  
$ `locate "NASA"`  >> `/home/nsl/NASA_access_log_Jul95.gz`

## Kernel processes
Starts some “automatic” processes   
Those processes have [brackets] around them in ps  
Starts the system management daemon  
  Process ID 1, “init”  
 
 init/systemd process  

---

## Init Process
 
Make sure the system is running the right services and daemons
 
Which services - defined by a certain mode or “runlevel”

Most common examples of runlevels:  
+ 1 Single-user mode (runlevel 1)
    + “Safe mode” - minimal filesystems, no services, root shell only (system recovery)
+ 5 Multi-user mode (runlevel 5)
    + Regular operation, all filesystems, network, services, graphics 
+ 3 Server mode (runlevel 3)
   + Similar to multi-user, but no graphics

---
 
### AT&T System V UNIX init
Circa 1983  

Layers and layers of shell scripts, cross-linked to runlevel-specific directories telling the system to run

No dependency model, so startup and shutdown scripts have to be run in a numeric order maintained by you, the administrator

Scripts can’t execute until everything ahead of them has finished, so they can’t run in parallel, so the system takes a long time to change state

## Replacements for init
init wasn’t really powerful enough to handle the needs of modern systems, and the benefits like multi-core and hyperthreading.
Ubuntu Upstart - circa 2009 - discontinued in 2016
systemd - circa 2010 - widely adopted in most modern Linux variants 

## How systemd works
Unified theory of how services should be configured, accessed, and managed
Like a package manager, defines a robust dependency model, not just for services but for “targets” (the new name for runlevels)
The scope creep is real - systemd also manages network (networkd), kernel logs (journald), and logins (logind)

## systemd units
More than just services - sockets, devices, mount points, startup items, watched filesystem paths, timers, resource management slices, externally created processes…
man systemd.unit
The unit file defines where the executable is, how to start it, stop it, and any dependencies it needs to run
systemd unit files: 
/lib/systemd/system/ - package installations, don’t modify
/etc/systemd/system/ - local customizations, highest priority

## A systemd unit file
[Unit]
Description=A high performance web server and a reverse proxy server
After=network.target

[Service]
Type=forking
PIDFile=/run/nginx.pid
ExecStartPre=/usr/bin/rm -f /run/nginx.pid
ExecStartPre=/usr/sbin/nginx -t
ExecStart=/usr/sbin/nginx
ExecReload=/bin/kill -s HUP $MAINPID
KillMode=process
KillSignal=SIGQUIT
TimeoutStopSec=5
PrivateTmp=true

[Install]
WantedBy=multi-user.target

## systemd unit file sections
[Unit] - This section contains the metadata and configurations of the relationship to other units
[Service] - This could be any unit type, but we care most about services.  This section configures how the service starts, runs, restarts, stops, etc.
[Install] - Optional, not interpreted during runtime.  Defines if the service is enabled or disabled (starts on boot), and what should happen when its enabled.

## systemctl - managing systemd

systemctl
By default, runs systemctl list-units
systemctl list-units --type=service
systemctl <enable|disable> <unit>
systemctl status <unit>
systemctl <start|stop|restart> <unit>
systemctl daemon-reload

```
   11  systemctl
   12  systemctl list-units --type-service
   13  systemctl --list-units --type-service
   14  systemctl list-units --type=service
   15  sudo systemctl enable nginx.service
   16  sudo apt-get install nginx
   17  sudo systemctl enable nginx.service
   18  NullSp4c3Lab5
   19  sudo systemctl enable nginx.service
   20  history
$ `systemctl status nginx`
```
● nginx.service - A high performance web server and a reverse proxy se
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor 
   Active: active (running) since Sat 2019-05-18 18:12:17 UTC; 2min 24
 Main PID: 18401 (nginx)
   CGroup: /system.slice/nginx.service
           ├─18401 nginx: master process /usr/sbin/nginx -g daemon on;
           └─18402 nginx: worker process   
```
$ sudo systemctl stop nginx
```
$ systemctl status nginx
● nginx.service - A high performance web server and a reverse proxy se
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor 
   Active: inactive (dead) since Sat 2019-05-18 18:17:07 UTC; 14s ago
  Process: 18644 ExecStop=/sbin/start-stop-daemon --quiet --stop --ret
 Main PID: 18401 (code=exited, status=0/SUCCESS)
```
```
Active: inactive (dead) since Sat 2019-05-18 18:17:07 UTC; 14s ag

#### If you are adding or editing unit files you need to use:  
$ `sudo systemctl daemon-reload`

Run level | Target | Description
0 | poweroff.target | System halt
1 (single) | rescue.target | Single-user mode
2 | multi-user.target | Multiuser mode (shell)
3
multi-user.target
Multiuser mode with networking
5
graphical.target
Multiuser mode + net + GUI
6
reboot.target
System reboot

$ `systemctl get-default`  
graphical.target

## Using targets
sudo systemctl isolate <target>
sudo systemctl isolate multi-user.target
Activates stated target and its dependencies, but deactivates all other units.
The old command to change runlevels was called telinit and some systems have a compatibility shim to make this work with systemctl.
See the default target: systemctl get-default
See all available targets: systemctl list-units --type=target

---

## systemd dependencies
Wants - Units that should be co-activated if possible, but not required
Requires - Strict dependencies; failure of any Requires terminates this service
Requisite, BindsTo, PartOf - Similar to Requires but work in different ways
Conflicts - Negative dependencies; cannot be co-active with these units
man systemd.service

---

## Systemd unit statuses
 bad
Some kind of problem with systemd, usually bad unit file
disabled
Present, but not configured to start automatically
enabled
Installed and runnable, will start automatically
indirect
Disabled, but has peers in “Also” clauses that may be enabled
linked
Unit file available through a symlink
masked
Banished from the systemd world from a logical perspective
static
Depended on by another unit; has no install requirements
```

## 23 Process Creation
Forking  
When you call a new process, the existing process is cloned, and then the clone can change the program it’s running for a different one.  
The original process is referred to as a parent, and then copy is called the child.  
PID - Process ID  
UID - The user ID who started the process  
EUID - “Effective” user ID, which user’s permissions are applied to the process  
GID - group id
EGID… effective group id

## ps - the live process listing
ps - shows processes for the current shell
ps -A or ps -e - Display every active process on a Linux system
ps aux - Display every process in the BSD format
ps -ef - Full-format listing (includes UID)
ps axf - tree-style view of process hierarchy (forest view)
```
 1178 ?     Ss  0:00 /usr/sbin/sshd -D
10784 ?     Ss  0:00  \_ sshd: jfineberg [priv]
10856 ?     S   0:00     \_ sshd: jfineberg@pts/0
10859 pts/0 Ss  0:00         \_ -bash
12789 pts/0 R+  0:00           \_ ps axf
```
pts - terminal device   
tty - terminal  (teletype)

## 25 ps aux output columns (man ps)
**USER** - process owner  
**PID** - process ID  
**%CPU** - Percentage of the CPU this process is using  
**%MEM** - Percentage of the real memory this process is using  
**VSZ** - Virtual size of the process (number of bytes allocated )  
**RSS** - (Sometimes displayed as RES) Resident set size (number of pages in memory)(block size)  
**TTY** - Control terminal ID  
**STAT** -  Status  
- | -
---|---
R | Runnable           
D | Uninterruptible sleep  
S | Sleeping             
T | Traced or stopped  
Z | Zombie  
**TIME** - CPU Time the process has consumed  
**COMMAND** - Command name and arguments (may have been modified by the process)

## 26 top - live updating processes and stats
**top** - find out what processes are running and how many resources they are consuming  
Real time system information
```
top - 
Tasks: 112 total,   1 running, 111 sleeping,   0 stopped,   0 zomb
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.
KiB Mem :  1014452 total,   141564 free,    72180 used,   800708 b
KiB Swap:        0 total,        0 free,        0 used.   728868 a
```
Interactive!  
    + q to quit
    + **q** to quit  
    + **h** for help  
**O** (capital o) for sort menu  
**z** to add color highlighting of running processes  
**d** to change refresh interval

---

## uptime
```
$ uptime
 19:11:26 up  1:50,  1 user,  load average: 0.00, 0.00, 0.00
$ uptime
 12:14:23 up  2:10,  1 user,  load average: 0.34, 0.35, 0.30
```
Current time, (19:11:26) how long the system has been running,  

How many users are logged on, and the system load averages.

System has been up for (`1:50`) one hour 50 minutes

System load averages occur as 3 numbers: the last 1, 5, and 15 minutes

Load averages are based on a single-core system,  
so if you have a quad-core system,  
your system can handle up to 4.0 load before it’s CPU bottlenecked.  
`load average: 0.34, 0.35, 0.30`

Check CPU utilization with top or ps to verify %.

[hyper-threading](https://en.wikipedia.org/wiki/Hyper-threading) - is Intel's proprietary simultaneous multithreading (SMT) implementation used to improve parallelization of computations (doing multiple tasks at once) performed on x86 microprocessors.

---

## 28 Process Signals

Signals are a form of inter-process communication.
You can stop, interrupt, or suspend processes with special control keys.
You can run a command (kill) to send signals to processes.
The kernel may notify a process of an “interesting” condition such as the death of a child process or the availability of data on an I/O channel.
A process “catches” a signal to handle for it.  A process might terminate upon getting a certain signal, or generate a core dump.

## Signals
**HUP** - Hangup
**INT** - Interrupt
**QUIT** - Quit
**KILL** - Kill
**SEGV** - Segmentation fault
**TERM** - Software termination
**STOP** - Stop
**WINCH** - Window Changed
**USR1** - User-defined #1
**USR2** - User-defined #2
**kill -l** - list all process signal options
```
nsl@linuxclass-007:~$ sudo apt install nginx
[sudo] password for nsl: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
nginx is already the newest version (1.10.3-0ubuntu0.16.04.3).
0 upgraded, 0 newly installed, 0 to remove and 26 not upgraded.
nsl@linuxclass-007:~$ pgrep nginx
nsl@linuxclass-007:~$ sudo pgrep nginx
nsl@linuxclass-007:~$ sudo systemctl start nginx
nsl@linuxclass-007:~$ sudo pgrep nginx
18771
18772
nsl@linuxclass-007:~$ sudo kill -l 18771 (sending a signal not hanging up)
HUP INT QUIT ILL TRAP ABRT BUS FPE KILL USR1 SEGV USR2 PIPE ALRM TERM STKFLT
CHLD CONT STOP TSTP TTIN TTOU URG XCPU XFSZ VTALRM PROF WINCH POLL PWR SYS

nsl@linuxclass-007:~$ sudo kill -HUP 18771
nsl@linuxclass-007:~$ sudo pgrep nginx
18771
18792
nsl@linuxclass-007:~$ ps aux | grep nginx
root     18771  0.0  0.4 125124  4264 ?        Ss   19:26   0:00 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
www-data 18792  0.0  0.3 125452  3196 ?        S    19:29   0:00 nginx: worker process
nsl      18796  0.0  0.1  12944  1088 pts/0    S+   19:30   0:00 grep --color=auto nginx

nsl@linuxclass-007:~$ kill -l
 1) SIGHUP   2) SIGINT   3) SIGQUIT  4) SIGILL   5) SIGTRAP
 6) SIGABRT  7) SIGBUS   8) SIGFPE   9) SIGKILL 10) SIGUSR1
11) SIGSEGV 12) SIGUSR2 13) SIGPIPE 14) SIGALRM 15) SIGTERM
16) SIGSTKFLT 17) SIGCHLD 18) SIGCONT 19) SIGSTOP 20) SIGTSTP
21) SIGTTIN 22) SIGTTOU 23) SIGURG  24) SIGXCPU 25) SIGXFSZ
26) SIGVTALRM 27) SIGPROF 28) SIGWINCH  29) SIGIO 30) SIGPWR
31) SIGSYS  34) SIGRTMIN  35) SIGRTMIN+1  36) SIGRTMIN+2  37) SIGRTMIN+3
38) SIGRTMIN+4  39) SIGRTMIN+5  40) SIGRTMIN+6  41) SIGRTMIN+7  42) SIGRTMIN+8
43) SIGRTMIN+9  44) SIGRTMIN+10 45) SIGRTMIN+11 46) SIGRTMIN+12 47) SIGRTMIN+13
48) SIGRTMIN+14 49) SIGRTMIN+15 50) SIGRTMAX-14 51) SIGRTMAX-13 52) SIGRTMAX-12
53) SIGRTMAX-11 54) SIGRTMAX-10 55) SIGRTMAX-9  56) SIGRTMAX-8  57) SIGRTMAX-7
58) SIGRTMAX-6  59) SIGRTMAX-5  60) SIGRTMAX-4  61) SIGRTMAX-3  62) SIGRTMAX-2
63) SIGRTMAX-1  64) SIGRTMAX  

nsl@linuxclass-007:~$ -1 -l
```
$ sudo kill -9 process# - hard kill a process

## 30 Process management
**pgrep <pattern>** - look up processes by name
**kill <pid>** - send SIGTERM signal to a process
**kill -HUP <pid>** - send “hangup” signal to an application - i.e. nginx uses this to reload configuration
**kill -KILL <pid>** - send SIGKILL process signal to the kernel instead - for “misbehaving” applications (kill -9)
**pkill <process_name>** - pgrep and kill in one command
**killall <process_name>** - terminate all processes matching process_name

### Controlling nginx
https://docs.nginx.com/nginx/admin-guide/basic-functionality/runtime-control/

```
$ uptime
 19:11:26 up  1:50,  1 user,  load average: 0.00, 0.00, 0.00
nsl@linuxclass-007:~$ kill -l
 1) SIGHUP   2) SIGINT   3) SIGQUIT  4) SIGILL   5) SIGTRAP
 6) SIGABRT  7) SIGBUS   8) SIGFPE   9) SIGKILL 10) SIGUSR1
11) SIGSEGV 12) SIGUSR2 13) SIGPIPE 14) SIGALRM 15) SIGTERM
16) SIGSTKFLT 17) SIGCHLD 18) SIGCONT 19) SIGSTOP 20) SIGTSTP
21) SIGTTIN 22) SIGTTOU 23) SIGURG  co24) SIGXCPU 25) SIGXFSZ
26) SIGVTALRM 27) SIGPROF 28) SIGWINCH  29) SIGIO 30) SIGPWR
31) SIGSYS  34) SIGRTMIN  35) SIGRTMIN+1  36) SIGRTMIN+2  37) SIGRTMIN+3
38) SIGRTMIN+4  39) SIGRTMIN+5  40) SIGRTMIN+6  41) SIGRTMIN+7  42) SIGRTMIN+8
43) SIGRTMIN+9  44) SIGRTMIN+10 45) SIGRTMIN+11 46) SIGRTMIN+12 47) SIGRTMIN+13
48) SIGRTMIN+14 49) SIGRTMIN+15 50) SIGRTMAX-14 51) SIGRTMAX-13 52) SIGRTMAX-12
53) SIGRTMAX-11 54) SIGRTMAX-10 55) SIGRTMAX-9  56) SIGRTMAX-8  57) SIGRTMAX-7
58) SIGRTMAX-6  59) SIGRTMAX-5  60) SIGRTMAX-4  61) SIGRTMAX-3  62) SIGRTMAX-2
63) SIGRTMAX-1  64) SIGRTMAX  
nsl@linuxclass-007:~$ 

```

## 32 The /proc filesystem
**Virtual filesystem** - “process information pseudo-filesystem” 
NullSp4c3Lab5 
```
$ ps aux | grep nginx
$ cd /proc/18771
$ cat cmdline
nginx: master process /usr/sbin/nginx -g daemon on; master_process
1$ sudo ls -l cwd
[sudo] password for nsl: 
lrwxrwxrwx 1 root root 0 May 18 20:11 cwd -> /
$ sudo ls -l environ
-r-------- 1 root root 0 May 18 20:11 environ
$ sudo ls -l exe
lrwxrwxrwx 1 root root 0 May 18 20:11 exe -> /usr/sbin/nginx
$ sudo ls -l fd
```

total 0
lrwx------ 1 root root 64 May 18 20:16 0 -> /dev/null
lrwx------ 1 root root 64 May 18 20:16 1 -> /dev/null
l-wx------ 1 root root 64 May 18 20:16 10 -> /var/log/nginx/error.log
l-wx------ 1 root root 64 May 18 20:16 2 -> /var/log/nginx/error.log
lrwx------ 1 root root 64 May 18 20:16 4 -> socket:[38319]
lrwx------ 1 root root 64 May 18 20:16 5 -> socket:[38320]
lrwx------ 1 root root 64 May 18 20:16 6 -> socket:[38129]
lrwx------ 1 root root 64 May 18 20:16 7 -> socket:[38130]
l-wx------ 1 root root 64 May 18 20:16 9 -> /var/log/nginx/access.
```

```
Doesn't contain 'real' files but runtime system information (e.g. system memory, devices mounted, hardware configuration, etc). 

A control and information center for the kernel. In fact, quite a lot of system utilities are simply calls to files in this directory.

By altering files located in this directory you can even read/change kernel parameters (sysctl) while the system is running.

## 33 The /proc filesystem, cont.
`/proc/${PID}/` - Numbered directories correspond to an actual process ID
`/proc/${PID}/cmdline` - Command-line arguments
`/proc/${PID}/cwd` - Link to current working directory
`/proc/${PID}/environ` - Values of environment variables 
`/proc/${PID}/exe` - Link to the executable 
`/proc/${PID}/fd/` - Directory of all the file descriptors held 

---

## 34 The /proc filesystem, cont. (again)
/proc/${PID}/status - Process status in human-readable form
Other system-wide proc files:
/proc/cpuinfo - Hardware CPU information
/proc/meminfo - Hardware memory information
man proc

## How to use /proc
Even though most of the files in `/proc` have a size of 0, you can read them!

`sudo cat /proc/${PID}/status`
`sudo cat /proc/18771/status`


Some of the `/proc/${PID}/` files are all scrunched up because they use null bytes instead of newlines.  Fix this by using “strings:” (To use string $ sudo apt install binutils)

`sudo strings /proc/${PID}/environ`  
sudo strings /proc/18771/environ >> master_process on;


Most of this filesystem is read-only, but some files can be changed to tweak the kernel without needing to recompile and reboot.

http://bit.ly/proc-filesystem

$ pgrep bash
17894

$ cd /proc/17894
nsl@linuxclass-007:/proc/17894$ ls
```
attr             environ    mem            pagemap      stat
autogroup        exe        mountinfo      personality  statm
auxv             fd         mounts         projid_map   status
cgroup           fdinfo     mountstats     root         syscall
clear_refs       gid_map    net            sched        task
cmdline          io         ns             schedstat    timers
comm             limits     numa_maps      sessionid    uid_map
coredump_filter  loginuid   oom_adj        setgroups    wchan
cpuset           map_files  oom_score      smaps
cwd              maps       oom_score_adj  stack
```

$ `cat /proc/cpuinfo`
```
processor : 0
vendor_id : GenuineIntel
cpu family  : 6
model   : 63
model name  : Intel(R) Xeon(R) CPU E5-2676 v3 @ 2.40GHz
stepping  : 2
microcode : 0x43
cpu MHz   : 2400.048
cache size  : 30720 KB
physical id : 0
siblings  : 1
core id   : 0
cpu cores : 1
apicid    : 0
initial apicid  : 0
fpu   : yes
fpu_exception : yes
cpuid level : 13
wp    : yes
flags   : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx rdtscp lm constant_tsc rep_good nopl xtopology pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand hypervisor lahf_lm abm invpcid_single kaiser fsgsbase bmi1 avx2 smep bmi2 erms invpcid xsaveopt
bugs    : cpu_meltdown spectre_v1 spectre_v2 spec_store_bypass l1tf
bogomips  : 4800.09
clflush size  : 64
cache_alignment : 64
address sizes : 46 bits physical, 48 bits virtual
power management:
```

$ `cat /proc/meminfo`
```
MemTotal:        1014452 kB
MemFree:          139140 kB
MemAvailable:     727016 kB
Buffers:          105628 kB
Cached:           566496 kB
SwapCached:            0 kB
Active:           429832 kB
Inactive:         283380 kB
Active(anon):      44176 kB
Inactive(anon):     2692 kB
Active(file):     385656 kB
Inactive(file):   280688 kB
Unevictable:        3652 kB
Mlocked:            3652 kB
SwapTotal:             0 kB
SwapFree:              0 kB
Dirty:                 8 kB
Writeback:             0 kB
AnonPages:         44784 kB
Mapped:            43336 kB
Shmem:              3348 kB
Slab:             129228 kB
SReclaimable:      98508 kB
SUnreclaim:        30720 kB
KernelStack:        2560 kB
PageTables:         3048 kB
NFS_Unstable:          0 kB
Bounce:                0 kB
WritebackTmp:          0 kB
CommitLimit:      507224 kB
Committed_AS:     424628 kB
VmallocTotal:   34359738367 kB
VmallocUsed:           0 kB
VmallocChunk:          0 kB
HardwareCorrupted:     0 kB
AnonHugePages:     12288 kB
CmaTotal:              0 kB
CmaFree:               0 kB
HugePages_Total:       0
HugePages_Free:        0
HugePages_Rsvd:        0
HugePages_Surp:        0
Hugepagesize:       2048 kB
DirectMap4k:       53248 kB
DirectMap2M:      995328 kB
```

---

## 36 Memory
free - total system memory in bytes - free -m to display as megabytes
vmstat - virtual memory stats
dmidecode - memory hardware information
egrep 'Mem|Cache|Swap' /proc/meminfo - show more memory information

---
## 37 I’m out of memory, help!
A special space on the disk may be reserved for “swap.”
When you run out of memory, the kernel will try to take memory pages and save them to the swap space on disk.  This process is called “thrashing,” and it’s super slow. 
cat /proc/sys/vm/swappiness - a value between 0 and 100, higher values indicate more likeliness to swap.
Your cloud instances have disabled swap for a variety of reasons.  If swap is not available, the kernel OOM killer mechanism kicks in and has to free memory by killing processes.

---

$ ps aux | grep environ
nsl      19214  0.0  0.0  12944  1008 pts/0    S+   20:25   0:00 grep --color=auto environ
nsl@linuxclass-007:/proc/18771$ pgrep bash
17894
nsl@linuxclass-007:/proc/18771$ cd /proc/17894

nsl@linuxclass-007:/proc/17894$ ls
attr             environ    mem            pagemap      stat
autogroup        exe        mountinfo      personality  statm
auxv             fd         mounts         projid_map   status
cgroup           fdinfo     mountstats     root         syscall
clear_refs       gid_map    net            sched        task
cmdline          io         ns             schedstat    timers
comm             limits     numa_maps      sessionid    uid_map
coredump_filter  loginuid   oom_adj        setgroups    wchan
cpuset           map_files  oom_score      smaps
cwd              maps       oom_score_adj  stack

nsl@linuxclass-007:/proc/17894$ sudo cat environ
LANG=en_US.UTF-8USER=nslLOGNAME=nslHOME=/home/nslPATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/gamesMAIL=/var/mail/nslSHELL=/bin/bashSSH_CLIENT=24.205.141.166 19150 22SSH_CONNECTION=24.205.141.166 19150 172.31.21.79 22SSH_TTY=/dev/pts/0TERM=xterm-256colorXDG_SESSION_ID=2XDG_RUNTIME_DIR=/

---

https://www.geeksforgeeks.org/proc-file-system-linux/

## [proc file system in Linux](https://docs.nginx.com/nginx/admin-guide/basic-functionality/runtime-control/)
Proc file system (procfs) is virtual file system created on fly when system boots and is dissolved at time of system shut down.

It contains the useful information about the processes that are currently running, it is regarded as control and information centre for kernel.

The proc file system also provides communication medium between kernel space and user space

https://www.tldp.org/LDP/Linux-Filesystem-Hierarchy/html/proc.html

---

## Memory
free - total system memory in bytes - free -m to display as megabytes  
vmstat - virtual memory stats  
dmidecode - memory hardware information  
egrep 'Mem|Cache|Swap' /proc/meminfo - show more memory information

$ `free`
```
$ free
              total        used        free      shared  buff/cache   available
Mem:        1014452       73884      163092        3348      777476      727160
Swap:             0           0           0
```

```
$ free  -m
              total        used        free      shared  buff/cache   available
Mem:            990          72         159           3         759         710
Swap:             0           0           0
```

free -m megabytes  
free -g gigabytes  
free -h human readable  

$ `sudo vmstat`
```
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 0  0      0 162308 104528 673112    0    0    44    92   27   51  1  0 99  0  0

```

$ `sudo dmidecode`
```
# dmidecode 3.0
Getting SMBIOS data from sysfs.
SMBIOS 2.7 present.
11 structures occupying 359 bytes.
Table at 0x000EB01F.

Handle 0x0000, DMI type 0, 24 bytes
BIOS Information
  Vendor: Xen
  Version: 4.2.amazon
  Release Date: 08/24/2006
  Address: 0xE8000
  Runtime Size: 96 kB
  ROM Size: 64 kB
  Characteristics:
    PCI is supported
    EDD is supported
    Targeted content distribution is supported
  BIOS Revision: 4.2

Handle 0x0100, DMI type 1, 27 bytes
System Information
  Manufacturer: Xen
  Product Name: HVM domU
  Version: 4.2.amazon
  Serial Number: ec2be5c8-51d3-f592-83d3-b40ad8e84b5a
  UUID: EC2BE5C8-51D3-F592-83D3-B40AD8E84B5A
  Wake-up Type: Power Switch
  SKU Number: Not Specified
  Family: Not Specified

Handle 0x0300, DMI type 3, 13 bytes
Chassis Information
  Manufacturer: Xen
  Type: Other
  Lock: Not Present
  Version: Not Specified
  Serial Number: Not Specified
  Asset Tag: Not Specified
  Boot-up State: Safe
  Power Supply State: Safe
  Thermal State: Safe
  Security Status: Unknown

Handle 0x0401, DMI type 4, 26 bytes
Processor Information
  Socket Designation: CPU 1
  Type: Central Processor
  Family: Other
  Manufacturer: Intel
  ID: F2 06 03 00 FF FB 89 17
  Version: Not Specified
  Voltage: Unknown
  External Clock: Unknown
  Max Speed: 2400 MHz
  Current Speed: 2400 MHz
  Status: Populated, Enabled
  Upgrade: Other

Handle 0x0B00, DMI type 11, 5 bytes
OEM Strings
  String 1: Xen

Handle 0x1000, DMI type 16, 19 bytes
Physical Memory Array
  Location: Other
  Use: System Memory
  Error Correction Type: Multi-bit ECC
  Maximum Capacity: 1 GB
  Error Information Handle: Not Provided
  Number Of Devices: 1

Handle 0x1100, DMI type 17, 34 bytes
Memory Device
  Array Handle: 0x1000
  Error Information Handle: 0x0000
  Total Width: 64 bits
  Data Width: 64 bits
  Size: 1024 MB
  Form Factor: DIMM
  Set: None
  Locator: DIMM 0
  Bank Locator: Not Specified
  Type: RAM
  Type Detail: None
  Speed: Unknown
  Manufacturer: Not Specified
  Serial Number: Not Specified
  Asset Tag: Not Specified
  Part Number: Not Specified
  Rank: Unknown
  Configured Clock Speed: Unknown

Handle 0x1300, DMI type 19, 31 bytes
Memory Array Mapped Address
  Starting Address: 0x00000000000
  Ending Address: 0x0003FFFFFFF
  Range Size: 1 GB
  Physical Array Handle: 0x1000
  Partition Width: 1

Handle 0x1400, DMI type 20, 35 bytes
Memory Device Mapped Address
  Starting Address: 0x00000000000
  Ending Address: 0x0003FFFFFFF
  Range Size: 1 GB
  Physical Device Handle: 0x1100
  Memory Array Mapped Address Handle: 0x1300
  Partition Row Position: 1

Handle 0x2000, DMI type 32, 11 bytes
System Boot Information
  Status: No errors detected

Handle 0x7F00, DMI type 127, 4 bytes
End Of Table
```

$ `egrep 'Mem|Cache|Swap' /proc/meminfo`

$ `alias mymem="egrep 'Mem|Cache|Swap' /proc/meminfo"`

---

## 37 Thrashing I’m out of memory, help!
A special space on the disk may be reserved for “swap.” 

When you run out of memory, the kernel will try to take memory pages and save them to the swap space on disk.  This process is called “thrashing,” and it’s super slow. 

`cat /proc/sys/vm/swappiness` - a value between 0 and 100, higher values indicate more likeliness to swap.

Your cloud instances have disabled swap for a variety of reasons.  If swap is not available, the kernel OOM killer mechanism kicks in and has to free memory by killing processes.

si (swap in)  
so (swap out)

```
$ cat /proc/sys/vm/swappiness
60
nsl@linuxclass-007:/$ free -m
              total        used        free      shared  buff/cache   available
Mem:            990          72         157           3         759         709
Swap:             0           0           0
nsl@linuxclass-007:/$ echo 10 | sudo tee /proc/sys/vm/swappiness
10
nsl@linuxclass-007:/$ cat /proc/sys/vm/swappiness
10
```
60 / 10 value between 0 and 100  

if the value is too low you'll hit the out of memory killer oomk  
if it is too high performance issues


tee splits it 2 ways  
man tee 
```
TEE(1)                    User Commands                   TEE(1)

NAME
       tee - read from standard input and write to standard out‐
       put and files
```

---

## Disk
**mount - display the physical and virtual disks attached to the system  
**df** - the current disk format allocation (df -h for human-readable sizes)  
**du** - disk usage by file and directory (du -h for human-readable sizes)  
**du -sh** - get summary of a directory  
**lsof** - list open files (lsof -p <PID> to search by process ID)  
**iotop** - top for file input/output, not installed by default, needs sudo  

**$ `mount`**  
```
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
udev on /dev type devtmpfs (rw,nosuid,relatime,size=499280k,nr_inodes=124820,mode=755)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,noexec,relatime,size=101448k,mode=755)
/dev/xvda1 on / type ext4 (rw,relatime,discard,data=ordered)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev)
tmpfs on /run/lock type tmpfs (rw,nosuid,nodev,noexec,relatime,size=5120k)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,mode=755)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,xattr,release_agent=/lib/systemd/systemd-cgroups-agent,name=systemd)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,perf_event)
cgroup on /sys/fs/cgroup/hugetlb type cgroup (rw,nosuid,nodev,noexec,relatime,hugetlb)
cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,cpu,cpuacct)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)
cgroup on /sys/fs/cgroup/pids type cgroup (rw,nosuid,nodev,noexec,relatime,pids)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,memory)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,blkio)
cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup (rw,nosuid,nodev,noexec,relatime,net_cls,net_prio)
cgroup on /sys/fs/cgroup/cpuset type cgroup (rw,nosuid,nodev,noexec,relatime,cpuset)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,freezer)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=29,pgrp=1,timeout=0,minproto=5,maxproto=5,direct)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,relatime)
debugfs on /sys/kernel/debug type debugfs (rw,relatime)
mqueue on /dev/mqueue type mqueue (rw,relatime)
fusectl on /sys/fs/fuse/connections type fusectl (rw,relatime)
/var/lib/snapd/snaps/amazon-ssm-agent_1068.snap on /snap/amazon-ssm-agent/1068 type squashfs (ro,nodev,relatime)
/var/lib/snapd/snaps/core_6673.snap on /snap/core/6673 type squashfs (ro,nodev,relatime)
lxcfs on /var/lib/lxcfs type fuse.lxcfs (rw,nosuid,nodev,relatime,user_id=0,group_id=0,allow_other)
/var/lib/snapd/snaps/core_6818.snap on /snap/core/6818 type squashfs (ro,nodev,relatime)
/var/lib/snapd/snaps/amazon-ssm-agent_1335.snap on /snap/amazon-ssm-agent/1335 type squashfs (ro,nodev,relatime)
tmpfs on /run/user/1001 type tmpfs (rw,nosuid,nodev,relatime,size=101448k,mode=700,uid=1001,gid=1001)
```

`/dev/xvda1 on / type ext4 (rw,relatime,discard,data=ordered)`  
xvd - solid state drive  
a - drive  
1 - partition  
type ext4 - file system type  

ro - read only  
rw  - read write  
relatime - access times ( The mount option relatime is a nice mix between noatime and atime and reduces write actions on the disk and still updates the atime of a file.)  


$ `find /dev -type b` (b is a block device)  
A block device is a computer data storage device that supports reading and (optionally) writing data in fixed-size blocks, sectors, or clusters. These blocks are generally 512 bytes or a multiple thereof in size.
```
/dev/xvda1
/dev/xvda
/dev/loop7
/dev/loop6
/dev/loop5
/dev/loop4
/dev/loop3
/dev/loop2
/dev/loop1
/dev/loop0
/dev/ram15
/dev/ram14
/dev/ram13
/dev/ram12
/dev/ram11
/dev/ram10
/dev/ram9
/dev/ram8
/dev/ram7
/dev/ram6
/dev/ram5
/dev/ram4
/dev/ram3
/dev/ram2
/dev/ram1
/dev/ram0
```

$ `df` (list of file systems and how close it is to full)  
```
$ df
Filesystem     1K-blocks    Used Available Use% Mounted on
udev              499280       0    499280   0% /dev
tmpfs             101448    3320     98128   4% /run
/dev/xvda1       8065444 1490412   6558648  19% /
tmpfs             507224       0    507224   0% /dev/shm
tmpfs               5120       0      5120   0% /run/lock
tmpfs             507224       0    507224   0% /sys/fs/cgroup
/dev/loop0         18304   18304         0 100% /snap/amazon-ssm-agent/1068
/dev/loop1         91392   91392         0 100% /snap/core/6673
/dev/loop2         91648   91648         0 100% /snap/core/6818
/dev/loop3         18432   18432         0 100% /snap/amazon-ssm-agent/1335
tmpfs             101448       0    101448   0% /run/user/1001
```

$ `df -h`  
```
Filesystem      Size  Used Avail Use% Mounted on
udev            488M     0  488M   0% /dev
tmpfs           100M  3.3M   96M   4% /run
/dev/xvda1      7.7G  1.5G  6.3G  19% /
tmpfs           496M     0  496M   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           496M     0  496M   0% /sys/fs/cgroup
/dev/loop0       18M   18M     0 100% /snap/amazon-ssm-agent/1068
/dev/loop1       90M   90M     0 100% /snap/core/6673
/dev/loop2       90M   90M     0 100% /snap/core/6818
/dev/loop3       18M   18M     0 100% /snap/amazon-ssm-agent/1335
tmpfs           100M     0  100M   0% /run/user/1001
```

---

## Network
**ifconfig** - network interface configuration and stats
**route** - network routing tables
**`/etc/resolv.conf`** - file that configures your DNS resolvers
**netstat** - see active network connections
**iftop** - top for network traffic, requires sudo
**tcpdump** - Capture network packets for troubleshooting and hacking :)


---

## Job control

---

## Niceness
+ Niceness is the priority of processes on a system and how the kernel allocates resources to them
+ Less nice = higher priority (more greedy, not as good at sharing)
+ More nice = lower priority (better at sharing resources)
+ “NI” column in top is the niceness of that process
+ -19 or -20 will be the least nice, 19 or 20 being the most nice
+ nice -n 15 [command_to_execute] - starts an application with 15 niceness
+ renice -n -10 -p [pid] - adjust the niceness of process


---

## Cron
cron is a system service that runs jobs on a schedule
Schedule is described in a file that we call “crontab”
crontab -l - list your crontab
crontab -e - edit your crontab
Located in /etc/crontab or /etc/cron.d/ subdirectories
Crontab looks like:


minute   hour   day   month   day-of-week   command
* = all values, , = multiple values
```
0 * * * * do_hourly_backup
0 2 * * 7 do_weekly_backup
30 0,4,8,12,16,20 * * * send_tweet
*/15 * * * * check_email
```

---

## 43 System logs
/var/log/syslog - the main system log
/var/log/auth.log - Authorizations, sudo, etc
/var/log/cron - Cron executions and errors
/var/log/daemon.log - Daemon facility messages
/var/log/debug - debugging output
/var/log/dmesg - Dump of the kernel message buffer
/var/log/faillog - Failed logins
/var/log/secure - Private authorizations, sshd, etc

## 44 journalctl - the systemd journal
journalctl - all messages from the systemd journal
journalctl -u <unit> - view journal logs from a specific unit
journalctl -u ssh
journalctl --disk-usage - view the disk usage of journal files on disk
journalctl -n 100 - view the last 100 entries
journalctl --since=yesterday


---

## 45 sysctl - changing kernel parameters
sysctl -a - print all sysctl variables
sysctl <variable> - view a specific variable
sysctl -w <variable>=<value> - write a variable value
You can also write variables the format <variable>=<value> into the /etc/sysctl.conf file or /etc/sysctl.d/ directory

---

## 46 Other programs you should know
wc - word count (characters, words, and lines)
cut - select certain parts of stdin based on delimiters and fields
sort - alphabetically sort from stdin
uniq - remove sequential duplicate lines (use with sort)
tar - create and extract archive files
curl, wget - make web requests
dig - query DNS

---

## 47 Great Books to check out
Unix and Linux System Administration Handbook, 5th Edition
How Linux Works: What Every Superuser Should Know, 2nd Edition
Learning the bash Shell: Unix Shell Programming
Essential System Administration
The Linux Programming Interface
CompTIA Linux+ Powered by Linux Professional Institute Study Guide

</details>

---


+ ssh -p 2022 jordan@obscurty

## [Class 1]()

<details><summary><ul><li>Intro to the command line & BASH</li>
  <li>Understanding the filesystem and managing files</li>
  <li>
  Input/Output between commands and files</li>
  <li>
  Using system documentation</li>
  <li>
  Installing new software</li>
  <ul></summary>

### Command Line Arguments

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


</details>

---

## [Class 2]()

<details><summary></summary>
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

### Manual pages
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

</details>
