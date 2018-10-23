# Linux-Essential

## Table of contents
* [Viewing/Monitoring Processes](https://github.com/Apostolovicka/Linux-Essential#viewingmonitoring-processes)
  * [ps](#ps---process-state)
  * [w](#w)
  * [top](#top)
  * [mpstat](#mpstat)
  * [uptime](#uptime)
  * [sar](#sar)

### Viewing/Monitoring Processes
> Every process on Linux has process ID or so called PID.

| Command | Description |
|---|---|
| **ps** | Detailed information about processes |
| **pstree** | A tree of processes and their connections |
| **top** | Monitor processes activity, dynamicaly updated |
| **uptime** | How long the system is running and the average load |
| **sar** | Infomation about system activity |
| **mpstat** | Multiple processor usage |
| **w** | List active processes for all users |
| TO ADD | iostat / numastat / strace |

#### PS - process state
>  Command reads information from the virtual files in /proc filesystem.
>  It displays information about your running processes, and with other options can show processes of other users.
>  The four items are labeled PID, TTY, TIME and CMD:
>    1. TIME is the amount of CPU time in minutes and seconds that the process has been running;
>    2. CMD is the name of the command that launched the process;
>    3. TTY (stands for terminal type) is the name of the console or terminal

```
> ps aux

USER               PID  %CPU %MEM      VSZ    RSS   TT  STAT STARTED      TIME COMMAND
root               221   2.1  0.1  4392220   9304   ??  Ss   13Oct18   0:54.41 /usr/libexec/TouchBarServer
apostolovicka     5585   1.7  2.2  5129056 180984   ??  R    11:14PM   0:06.21 /Applications/Utilities/Terminal
apostolovicka      271   1.6  0.7  5032336  57800   ??  S    13Oct18   0:46.65 /System/Library/CoreServices/Finder
```
options:
* **A** , **e** - information about other users' processes, including those without controlling terminals
* **a** - information about other users' processes as well as your own, skip any processes which do not have a
        controlling terminal, unless the -x option is also provided
* **f** - display the uid, pid, parent pid, recent CPU usage, process start time, controlling tty, elapsed CPU usage,
        and the associated command
* **u** - display the processes belonging to the specified usernames
* **x** - include processes which do not have a controlling terminal (TT = ??) - adds to the list processes that have   
        no controlling terminal, such as daemons, which are programs that are launched during booting

### TOP 
> man: Top command displays and update sorted information about processes
> Use this tool to determine which processes are running and how much memory and CPU they consume

```
> top

Processes: 361 total, 2 running, 359 sleeping, 1498 threads              
Load Avg: 1.75, 1.67, 1.72  CPU usage: 5.79% user, 5.31% sys, 88.88% idle   
SharedLibs: 204M resident, 38M data, 26M linkedit. 
MemRegions: 67445 total, 1655M resident, 94M private, 1998M shared.
PhysMem: 7432M used (1922M wired), 759M unused. 
VM: 1588G vsize, 1314M framework vsize, 10691703(0) swapins, 11168532(0) swapouts. 
Networks: packets: 12679845/17G in, 4086770/644M out.
Disks: 1318400/62G read, 1232193/60G written.

PID   COMMAND      %CPU TIME      #TH   #WQ  #PORT  MEM     PURG   CMPRS  PGRP PPID STATE     BOOSTS      %CPU_ME  %CPU_OTHRS 
7017  top          3.4  00:00.93  1/1   0    25     5704K+  0B     0B     7017 5587 running   *0[1]       0.00000  0.00000     
7011  Google Chrom 0.0  00:00.10  13    1    92     13M     4096B  0B     3464 3464 sleeping  *0[2]       0.00000  0.00000    

UID    FAULTS   COW       MSGSENT    MSGRECV   SYSBSD    SYSMACH    CSW
7319+  115      295016+   147487+    22369+    186589+   964+       0
501    9447     1709      207        82        1530      512        582
```

### MPSTAT
> man: The mpstat command lists activities for each available processor, processor 0 being the first one. 
> Global average activities among all processors are also reported.

```
> mpstat -P ALL

Linux 3.2.0-57-generic (USERNB01) 12/12/2013 _x86_64_ (2 CPU)

04:07:36 PM  CPU  %usr   %nice  %sys  %iowait %irq  %soft %steal %guest %idle
04:07:36 PM  all  6.02   0.04   1.72  2.99    0.00  0.05  0.00   0.00   89.17
04:07:36 PM  0    3.84   0.01   1.15  3.72    0.00  0.06  0.00   0.00   91.21
04:07:36 PM  1    13.55  0.15   3.66  0.46    0.00  0.03  0.00   0.00   82.15
```

Described output of the command:
* 03:29:29 PM : means the time that mpstat was run
* all : means All CPUs
* %usr : percentage of CPU utilization that occurred while executing at the user level (application)
* %nice : percentage of CPU utilization that occurred while executing at the user level with nice priority
* %sys : percentage of CPU utilization that occurred while executing at the system level (kernel)
* %iowait : percentage of time that the CPU or CPUs were idle during which the system had an outstanding disk I/O request
* %irq : percentage of time spent by the CPU or CPUs to service hardware interrupts
* %soft : percentage of time spent by the CPU or CPUs to service software interrupts
* %steal : percentage of time spent in involuntary wait by the virtual CPU or CPUs while the hypervisor was servicing another virtual processor
* %guest : show the percentage of time spent by the CPU or CPUs to run a virtual processor
* %idle : show the percentage of time that the CPU or CPUs were idle and the system did not have an outstanding disk I/O equest

### SAR
> TheGeekStuff: Using sar you can monitor performance of various Linux subsystems (CPU, Memory, I/O..) in real time.
> Using sar, you can also collect all performance data on an on-going basis, store them, and do historical analysis to
> identify bottlenecks.

Example below gives the system CPU statistics 3 times (with 1 second interval):
```
> sar 1 3

01:27:32 PM       CPU     %user     %nice   %system   %iowait    %steal     %idle
01:27:33 PM       all      0.00      0.00      0.00      0.00      0.00    100.00
01:27:34 PM       all      0.25      0.00      0.25      0.00      0.00     99.50
01:27:35 PM       all      0.75      0.00      0.25      0.00      0.00     99.00
Average:          all      0.33      0.00      0.17      0.00      0.00
```

More into on SAR command: [The Geek Stuff - SAR Examples](#https://www.thegeekstuff.com/2011/03/sar-examples/?utm_source=feedburner)

### UPTIME
> How long is the system running since the last boot.

```
> uptime

0:22  up 10 days,  9:56, 2 users, load averages: 1.54 1.51 1.62
```
Current time: 0:22
System time: up 10 days, 9 hours, 56 minutes
Logged users: 2
Load average in for three time periods: one minute (1.54), five minutes (1.51), fifteen minutes (1.62)
Load average is the average number of processes ready to run in that time interval.

### W
> Wiki: The command w on many Unix-like operating systems provides a quick summary of every user logged into a computer,
> what each user is currently doing, and what load all the activity is imposing on the computer itself. 
> The command is a one-command combination of several other Unix programs: who, uptime, and ps -a 

```
> w

11:12am up 608 day(s), 19:56,  6 users,  load average: 0.36, 0.36, 0.37
User     tty       login@   idle   what
smithj   pts/5      8:52am         w
jonesm   pts/23    20Apr06    28   -bash
harry    pts/18     9:01am     9   pine
peterb   pts/19    21Apr06         emacs -nw html/index.html
janetmcq pts/8     10:12am  3days  -csh
singh    pts/12    16Apr06   5:29  /usr/bin/perl -w perl/test/program.pl
```
