---
title: linux-ps
date: 2018-04-19 13:03:46
categories:
  - linux
tags:
  - linux
  - shell
  - command

---

**ps** (**processes status**) is a native Unix/Linux utility for viewing information concerning a selection of running processes on a system: it reads this information from the virtual files in [/proc filesystem](https://www.tecmint.com/exploring-proc-file-system-in-linux/). It is one of the important utilities for system administration specifically under process monitoring, to help you understand whats is going on a Linux system.

It has numerous options for manipulating its output, however you’ll find a small number of them practically useful for daily usage.

In this article, we’ll look at 30 useful examples of ps commands for monitoring active running processes on a Linux system.

Note that **ps** produces output with a heading line, which represents the meaning of each column of information, you can find the meaning of all the labels in the **ps man page**.

### List All Processes in Current Shell

**1.** If you run **ps command** without any arguments, it displays processes for the current shell.

```
$ ps 
```

List Current Running Processes

### Print All Processes in Different Formats

**2.** Display every active process on a Linux system in generic (Unix/Linux) format.

```
$ ps -A
OR
$ ps -e
```

List Processes in Standard Format

**3.** Display all processes in **BSD** format.

```
$ ps au
OR
$ ps axu
```

List Processes in BSD Format

**4.** To perform a full-format listing, add the `-f` or `-F` flag.

```
$ ps -ef
OR
$ ps -eF
```

List Processes in Long List Format

### Display User Running Processes

**5.** You can select all processes owned by you (runner of the **ps command**, root in this case), type:

```
$ ps -x 
```

**6.** To display a user’s processes by real user ID (**RUID**) or name, use the `-U` flag.

```
$ ps -fU tecmint
OR
$ ps -fu 1000
```

List User Processes by ID

**7.** To select a user’s processes by effective user **ID** (**EUID**) or name, use the `-u` option.

```
$ ps -fu tecmint
OR
$ ps -fu 1000
```

### Print All Processes Running as Root (Real and Effecitve ID)

**8.** The command below enables you to view every process running with **root** user privileges (real & effective ID) in user format.

```
$ ps -U root -u root 
```

Display Root User Running Processes

### Display Group Processes

**9.** If you want to list all processes owned by a certain group (real group ID (**RGID**) or name), type.

```
$ ps -fG apache
OR
$ ps -fG 48
```

Display Group Processes

**10.** To list all processes owned by effective group name (or session), type.

```
$ ps -fg apache
```

### Display Processes by PID and PPID

**11.** You can list processes by **PID** as follows.

```
$ ps -fp 1178
```

List Processes by PID

**12.** To select process by **PPID**, type.

```
$ ps -f --ppid 1154
```

List Process by PPID

**13.** Make selection using **PID** list.

```
$ ps -fp 2226,1154,1146
```

List Processes by PIDs

### Display Processes by TTY

**14.** To select processes by **tty**, use the **-t** flag as follows.

```
$ ps -t pst/0
$ ps -t pst/1
$ ps -ft tty1
```

List Processes by TTY

### Print Process Tree

**15.** A process tree shows how processes on the system are linked to each other; processes whose parents have been killed are adopted by the init (or systemd).

```
$ ps -e --forest 
```

List Process Tree

**16.** You can also print a process tree for a given process like this.

```
$ ps -f --forest -C sshd
OR
$ ps -ef --forest | grep -v grep | grep sshd 
```

List Tree View of Process

### Print Process Threads

**17.** To print all threads of a process, use the `-H` flag, this will show the **LWP** (**light weight process**) as well as **NLWP** (**number of light weight process**) columns.

```
$ ps -fL -C httpd
```

List Process Threads

### Specify Custom Output Format

Using the **-o** or **–format** options, ps allows you to build user-defined output formats as shown below.

**18.** To list all format specifiers, include the `L` flag.

```
$ ps L
```

**19.** The command below allows you to view the **PID**, **PPID**, user name and command of a process.

```
$ ps -eo pid,ppid,user,cmd
```

List Processes with Names

**20.** Below is another example of a custom output format showing file system group, nice value, start time and elapsed time of a process.

```
$ ps -p 1154 -o pid,ppid,fgroup,ni,lstart,etime
```

List Process ID Information

**21.** To find a [process name using its PID](https://www.tecmint.com/find-process-name-pid-number-linux/).

```
$ ps -p 1154 -o comm=
```

Find Process using PID

### Display Parent and Child Processes

**22.** To select a specific process by its name, use the -C flag, this will also display all its child processes.

```
$ ps -C sshd
```

Find Parent Child Process

**23.** Find all **PIDs** of all instances of a process, useful when writing scripts that need to read **PIDs** from a std output or file.

```
$ ps -C httpd -o pid=
```

Find All Process PIDs

**24.** Check execution time of a process.

```
$ ps -eo comm,etime,user | grep httpd
```

The output below shows the HTTPD service has been running for 1 hours, 48 minutes and 17 seconds.

Find Process Uptime

### Troubleshoot Linux System Performance

If your system isn’t working as it should be, for instance if it’s unusually slow, you can [perform some system troubleshooting](https://www.tecmint.com/linux-system-monitoring-troubleshooting-tools/) as follows.

**26.** Find [top running processes](https://www.tecmint.com/find-linux-processes-memory-ram-cpu-usage/) by highest memory and CPU usage in Linux.

```
$ ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head
OR
$ ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head
```

Find Top Running Processes

**27.** To kill an Linux [processes/unresponsive applications](https://www.tecmint.com/kill-processes-unresponsive-programs-in-ubuntu/) or any process that is consuming high CPU time.

First, find the **PID** of the unresponsive process or application.

```
$ ps -A | grep -i stress
```

Then use the [kill command](https://www.tecmint.com/how-to-kill-a-process-in-linux/) to terminate it immediately.

```
$ kill -9 2583 2584
```

Find and Kill a Process

### Print Security Information

**28.** Show security context (specifically for **SELinux**) like this.

```
$ ps -eM
OR
$ ps --context
```

Find SELinux Context

**29.** You can also display security information in user-defined format with this command.

```
$ ps -eo  euser,ruser,suser,fuser,f,comm,label
```

List SELinux Context by Users

### Perform Real-time Process Monitoring Using Watch Utility

**30.** Finally, since **ps** displays static information, you can employ the [watch utility](https://www.tecmint.com/fswatch-monitors-files-and-directory-changes-modifications-in-linux/) to perform real-time process monitoring with repetitive output, displayed after every second as in the command below (specify a custom **ps command** to achieve your objective).

```
$ watch -n 1 'ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head'
```

Real Time Process Monitoring

**Important**: ps only shows static information, to view frequently updated output you can use tools such as [htop](https://www.tecmint.com/install-htop-linux-process-monitoring-for-rhel-centos-fedora/); [top](https://www.tecmint.com/12-top-command-examples-in-linux/) and [glances](https://www.tecmint.com/glances-an-advanced-real-time-system-monitoring-tool-for-linux/): the last two are in fact Linux system performance monitoring tool.