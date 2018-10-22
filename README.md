# Linux-Essential

## Table of contents
* [Viewing/Monitoring Processes](https://github.com/Apostolovicka/Linux-Essential#viewingmonitoring-processes)
  * [ps - process state](#ps-process-state)

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
[options]: [A][e] - information about other users' processes, including those without controlling terminals
           [a] - information about other users' processes as well as your own, skip any processes which do not have a
                 controlling terminal, unless the -x option is also provided
           [f] - display the uid, pid, parent pid, recent CPU usage, process start time, controlling tty, elapsed CPU usage,
                 and the associated command
           [u] - display the processes belonging to the specified usernames
           [x] - include processes which do not have a controlling terminal (TT = ??) - adds to the list processes that have   
                 no controlling terminal, such as daemons, which are programs that are launched during booting
