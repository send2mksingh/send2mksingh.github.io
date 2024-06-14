---
layout: post
title: How Process Works...........
---


**Processe in Linux/Unix**

 We run a command or script it creates a process.

Whenever a command is issued in Unix/Linux, it creates/starts a new process. For example, pwd when issued which is used to list the current directory location the user is in, a process starts.
Through a 5 digit ID number Unix/Linux keeps an account of the processes, this number is called process ID or PID. 

Each process in the system has a unique PID.
Used up pid’s can be used in again for a newer process since all the possible combinations are used.

At any point of time, no two processes with the same pid exist in the system because it is the pid that Unix uses to track each process.

**Processes can be run in two ways-**

Type:1 Foreground Processes : Every process when started runs in foreground by default, receives input from the keyboard, and sends output to the screen.  When issuing pwd command.

- $pwd   
- This is going to run on foreground, simply on terminal and gives the output on terminal only that is standard output also.

When a command/process is running in the foreground/terminal and is taking a lot of time, no other processes can be run or started because the prompt would not be available until the program finishes processing and comes out.


Type2: Background Process: It runs in the background without keyboard input and waits till keyboard input is required. Thus, other processes can be done in parallel with the process running in the background since they do not have to wait for the previous process to be completed. 

Need to add & along with the command starts it as a background process

- $pwd &   
- This will run in background so that we can we on terminal and it will complete the execution in the background only.

**How to track ongoing processes:**

ps (Process status) can be used to see/list all the running processes.

- $ps 


more information -f (full) can be used along with ps  

- $ps -f


single-process information, ps along with process id is used 

- $ps pid

For a running program (named process) Pidof finds the process id’s (pids) 

$pidof process-name

**Meaning of Fields:**
- UID: User ID that this process belongs to - the person running it.

- PID: Process ID

- PPID: Parent process ID - the ID of the process that started it
- C  CPU utilization of process
- STIME Process start time
- TTY  Terminal type associated with the process
- TIME  CPU time is taken by the process
- CMD  The command that started this process

**Other important options can be used with ps to get more info about process**

- a  Shows information about all users
- x  Shows information about processes without terminals
- u  Shows additional information like -f option
- e  Displays extended information

**To stop a process:**

When running in foreground, hitting Ctrl + c (interrupt character) will exit the command. For processes running in background kill command can be used if it’s pid is known.

- $kill pid
- $kill -9 pid  - To kill a process forcefully.


- To check about the jobs running in background or stopped.
- $jobs 

- To resume a stopped job in backgroud -
- $bg 

- To resume a stopped job in foreground or terminal-
- $fg

**Top command gives the better details about all the process**

- $top

- Niceness Index or nice value is used to give priority to a process -
- $ nice -nice_value process_name

- It ranges from -20 to 19 where -20 it the highest value and 19 is the lowest value.
0 is the default value.

- Only the Admin user can add negative values, normal users can allocate only positive values to their processes.

**Usage of renice** 

- To change the priority of an already running process renice is used. 
- Syntax:  

- renice [-nice value] [process id]

**About Process Priority**

The kernel stores a great deal of information about processes including process priority which is simply the scheduling priority attached to a process. Processes with a higher priority will be executed before those with a lower priority, while processes with the same priority are scheduled one after the next, repeatedly.

PR value or priority is basically a no. that is used to give preferences for execution - suppose
we are running a process and its value is high then it is going to have early execution as compared to other process - its value from 0 to 139.
Where 0 to 99 for real time and 100 to 139 for user-space. 

- If the process priority is high thenn it will it will get more CPU time.




***KEEP LEARNING***