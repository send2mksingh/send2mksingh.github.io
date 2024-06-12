---
layout: post
title: Linux Basics
---

**05-06-2024**

**Usage of sed command** 

Stream editor - with the help of this command we can perform some tasks eg: lines printing, lines deleting, insert any line after and befor of any other lines, find and replace works.
Syntax - sed  <operations>   <file-name>
<any command name>   |  sed <operations> 

 > - to redirect output into file
 >> - to append output to into any existing file
 | - pipe signed is used to combine two or more commands to get desired output where output of 1st command is the input for the second command.
 

**Usage of Cut command**
It's text processing command used to cut records on the basis of characters, fields and delimeters separated.
Syntax - cut <options>  file-name.


**Usage of awk**
This is also text processing command can be used same as cut command.
- Syntax - awk <options>  file-name.

**Vim Editor**
- It is one of the popular text editor, with the help of vim we can create, edit files.
- It has basically four working modes eg:- normal mode, insert mode, command mode and visual mode.
- Esc key used to go to normal mode, i to insert mode, : to command mode and v to visual mode.

ls - list directory contents
pwd - print working directory
which - gives the path or location of commands or binary files
whatis - gives the shorts info about commands
su - to switch users
mkdir - to create new directory
cd - change directory
touch - create empty files
less - to read long files
more - to read long files
tree - list directory contents in tree format
whoami - tells the user name who logged in
uptime - cpu load average details
date - to check date
cal - print calender
bc - open binary calculator 
free - to check Ram and swap memory details
df - disk free details with file system
du - size of files and directory