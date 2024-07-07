---
 layout: post
 title: Zombie Process
 ---
   
  - A zombie process in Linux is a process that has completed execution but still has an entry in the process table. This happens because the process's parent hasn't read its exit status yet. Zombie processes can be problematic if they accumulate, as they consume process table entries, which are limited resources.

  **How a Zombie Process is Created**
  When a process completes its execution, it sends a SIGCHLD signal to its parent process. The parent process is supposed to read the exit status of the child process using the wait() system call. If the parent process does not call wait(), the child process remains in the zombie state.

  **Identifying Zombie Processes**
 ---
  You can identify zombie processes using the ps command. Zombie processes will have a status of Z.

 ----

  - bash
  - ps aux | grep Z


  Example of Creating a Zombie Process
 ---
  Here's a simple example to demonstrate a zombie process. We'll create a parent process that spawns a child process and intentionally does not wait for the child process to exit.

 ---
  - bash
  - #!/bin/bash
  - # Parent process
  - echo "Parent PID: $$"

  - # Child process
  - ( 
  - sleep 5
  - echo "Child process complete"
  - ) &

 # List processes
 ps -l
 In this script, the parent process does not call wait(), so after the child process finishes, it becomes a zombie.

 Handling Zombie Processes
 1. Wait for the Parent to Clean Up

 ---
  The best way to handle zombie processes is to ensure the parent process correctly waits for its children to exit.

---
 - #!/bin/bash
 - Parent process
 - echo "Parent PID: $$"

 - Child process
 - ( 
 -  sleep 5
 - echo "Child process complete"
 - ) &


 # Wait for child processes to exit
 -   wait

 # List processes
 - ps -l

 2. Kill the Parent Process
 -  If the parent process is not responding and accumulating zombie processes, you might need to kill  it. When the parent process is killed, its child processes are adopted by the init process, which properly cleans up zombies.

 ---
  Find the parent process ID (PID):

 ---
 - bash
 - Copy code
 - ps -ef | grep <parent_process_name>
 
--- 
- Kill the parent process:

---

 - bash
 - Copy code
 - sudo kill -9 <parent_process_pid>


3. Using wait in Scripts
Ensure your scripts always clean up child processes by using the wait command.

---
  Check the below script:

---

 - bash
 - Copy code
 - #!/bin/bash

 - start_child_process() {
 - (
 -   sleep 5
 -   echo "Child process $1 complete"
 -  ) &
 -  }

 - start_child_process 1
 - start_child_process 2


# Wait for all child processes to finish
wait
Summary
Zombie processes are processes that have finished execution but still have an entry in the process table because their parent hasn't read their exit status.
Identifying zombies can be done using ps aux | grep Z.
Handling zombies involves ensuring the parent process waits for its children or, in some cases, killing the parent process to allow init to adopt and clean up the zombies.
By understanding and managing zombie processes, you can ensure that your system remains efficient and doesn't run into issues due to process table saturation.





 

  