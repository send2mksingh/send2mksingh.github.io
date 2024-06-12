---
layout:post
title: Shell Scripting
---

**Comment in script**

Comments are often used to give message related to particular command.
Single line comment - add just #
eg:-  # this is simple script 

Multi lines script to give long details about the work or commands.
eg:- <<Comment
This is script 
written to use further 
comment  - end with same name as used for starting.

**Variables**

Variables are simply used to store values.

**Different types**

Local Variables − A local variable is a variable that is present within the current instance of the shell. It is not available to programs that are started by the shell. They are set at the command prompt.

Environment Variables − An environment variable is available to any child process of the shell. Some programs need environment variables in order to function correctly. Usually, a shell script defines only those environment variables that are needed by the programs that it runs.


a=10
b=20
echo $a   - calling the value
it will output 10

script example  --

eg: #!/bin/bash

NAME="Zara Ali"
echo $NAME

Environment variable or System defined variables  :
To make permanent changes to the environment variables for all new accounts, go to your /etc/skel files, such as .bashrc, and change the ones that are already there or enter the new ones. When you create new users, these /etc/skel files will be copied to the new user's home directory.

env   - command to display system variable


Constant variable are example of fix variable, that will not change in the script later.
eg:-   readonly variable=value


eg:  #!/bin/sh

NAME="Zara Ali"
readonly NAME
NAME="Qadiri"
