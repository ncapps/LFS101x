# Chapter 9: Processes

## Process Types

Process Type | Description | Example
--- | --- | ---
Interactive Processes | Need to be started by a user, either at a command line or through a graphical interface such as an icon or a menu selection |bash, firefox, top
Batch Processes | Automatic processes which are scheduled from and then disconnected from the terminal. These tasks are queued and work on a FIFO (First-In, First-Out) basis. | updatedb, ldconfig
Daemons	| Server processes that run continuously. Many are launched during system startup and then wait for a user or system request indicating that their service is required.	| httpd, sshd, libvirtd
Threads	| Lightweight processes. These are tasks that run under the umbrella of a main process, sharing memory and other resources, but are scheduled and run by the system on an individual basis. An individual thread can end without terminating the whole process and a process can create new threads at any time. Many non-trivial programs are multi-threaded. | firefox, gnome-terminal-server
Kernel Threads | Kernel tasks that users neither start nor terminate and have little control over. These may perform actions like moving a thread from one CPU to another, or making sure input/output operations to disk are completed. | kthreadd, migration, ksoftirqd

## Process and Thread IDs
ID Type | Description
--- | ---
Process ID (PID) | Unique Process ID number
Parent Process ID (PPID) | Process (Parent) that started this process. If the parent dies, the PPID will refer to an adoptive parent; on recent kernels, this is kthreadd which has PPID=2.
Thread ID (TID) | Thread ID number. This is the same as the PID for single-threaded processes. For a multi-threaded process, each thread shares the same PID, but has a unique TID.

## Terminating a Process
```sh
# Terminate a process
 kill -SIGKILL <pid>
 # OR
 kill -9 <pid>.
```

## More About Priorities
- The priority for a process can be set by specifying a **nice** value, or niceness, for the process.
- The lower the nice value, the higher the priority. Low values are assigned to important processes, while high values are assigned to processes that can wait longer.
- A process with a high nice value simply allows other processes to be executed first.

## Load Averages
- Short-term increases are usually not a problem. A high peak you see is likely a burst of activity, not a new level. For example, at start up, many processes start and then activity settles down. If a high peak is seen in the 5 and 15 minute load averages, it may be cause for concern.
```sh
# Show who is logged on and what they are doing.
$ w

# Display Linux processes
$ top

# Tell how long the system has been running.
$ uptime
```

## Background and Foreground Processes and Managing Jobs
- Linux supports background and foreground job processing. A job in this context is just a command launched from a terminal window.
- By default, all jobs are executed in the foreground. You can put a job in the background by suffixing & to the command, for example: `updatedb &`.
- The `jobs` utility displays all jobs running in background. The display shows the job ID, state, and command name, as shown here.
- The background jobs are connected to the terminal window, so, if you log off, the jobs utility will not show the ones started from that window.
```sh
$ sleep 100 &

$ jobs -l
```

## The `ps` Command
- `ps` provides information about currently running processes keyed by PID. If you want a repetitive update of this status, you can use `top` or other commonly installed variants (such as `htop` or `atop`)
- `pstree` displays the processes running on the system in the form of a tree diagram showing the relationship between a process and its parent process and any other processes that it created. Repeated entries of a process are not displayed, and threads are displayed in curly braces.
- use `top` to get constant real-time updates (every two seconds by default) of system performance
- You need to monitor memory usage very carefully to ensure good system performance. Once the physical memory is exhausted, the system starts using swap space (temporary storage space on the hard drive) as an extended memory pool, and since accessing disk is much slower than accessing memory, this will negatively affect system performance.

## Interactive Keys with `top`
- `top` can be utilized interactively for monitoring and controlling processes

Command | Output
--- | ---
t | Display or hide summary information (rows 2 and 3)
m | Display or hide memory information (rows 4 and 5)
A | Sort the process list by top resource consumers
r | Renice (change the priority of) a specific processes
k | Kill a specific process
f | Enter the top configuration screen
o | Interactively select a new sort order in the process list

## Scheduling Future Processes
- You can use the `at` utility program to execute any non-interactive command at a specified time
- `cron` is a time-based scheduling utility program. It can launch routine background jobs at specific times and/or days on an on-going basis. `cron` is driven by a configuration file called `/etc/crontab` (cron table)
- `sleep` suspends execution for at least the specified period of time, which can be given as the number of seconds (the default), minutes, hours, or days. After that time has passed (or an interrupting signal has been received), execution will resume.
```sh
$ at now + 2 days
at> touch file1.txt
```

## Summary
- Processes are used to perform various tasks on the system.
- Processes can be single-threaded or multi-threaded.
- Processes can be of different types, such as interactive and non-interactive.
- Every process has a unique identifier (PID) to enable the operating system to keep track of it.
- The nice value, or niceness, can be used to set priority.
- `ps` provides information about the currently running processes.
- You can use top to get constant real-time updates about overall system performance, as well as information about the processes running on the system.
- Load average indicates the amount of utilization the system is under at particular times.
- Linux supports background and foreground processing for a job.
- `at` executes any non-interactive command at a specified time.
- `cron` is used to schedule tasks that need to be performed at regular intervals.
