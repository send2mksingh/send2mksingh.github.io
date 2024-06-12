---
layout: post
title: Linux Terminology
---

The kernel is considered the brain of the Linux operating system. It controls the hardware and makes the hardware interact with the applications. An example of a kernel is the Linux kernel. The most recent Linux kernel, along with past Linux kernels, can be found at the kernel.org web site.

A distribution also known as Distros is a collection of programs combined with the Linux kernel to make up a Linux-based operating system. Some common examples of a distribution are Red Hat Enterprise Linux, Fedora, Ubuntu, and Gentoo.

The boot loader, as the name implies, is a program that boots the operating system. Two examples of a boot loader are GRUB and ISOLINUX.
A service is a program that runs as a background process. Some examples of the service are httpd, nfsd, ntpd, ftpd and named.

A filesystem is a method for storing and organizing files in Linux. Some examples of filesystems are ext3, ext4, FAT, XFS and Btrfs.
The X Window System provides the standard toolkit and protocol to build graphical user interfaces on nearly all Linux systems.
T- he desktop environment is a graphical user interface on top of the operating system. GNOME, KDE, Xfce and Fluxbox are some examples of the desktop environment.

The command line is an interface for typing commands on top of the operating system.
The Shell is the command line interpreter that interprets the command line input and instructs the operating system to perform any necessary tasks and commands. For example, bash, tcsh and zsh.


********TAR  [ Tape archive] *************
******************************************

- Tar command basically use to create archive and compress n number of files and directory.
- Archive    ==> collection of file and folder into a single tar file.


- Compress   ==> data Size will be compress , it will help in storage concept so that it will use less space rather then the actual size.--- 
- tar command basically support these compresstion method :-
---
- gzip    OR  .gz     ==> gunzip              ===>  -z   [ small z ]
- bzip2   OR   .bz2   ==> bunzip version 2    ===>  -j   [ small j ]
- xz      OR   .xz    ==> xz                  ===>  -J   [ caps J ]

- Note: If we are not using any option with tar command in that case it will create only the tar file.
      we can use anyone options as per demands to compress any tar file or actual file.


**Syntax:**

- #  tar   <options>     <arvice-name>     <name of the files and directory>
- c    ==> create archive
- x    ==> Extract
- r    ==> Append
- v    ==> verbose
- f    ==> From File  [ Mandatory ]
- t    ==> to check data listing of any tar file
- C  [capital C] ==>  to change the extract location 

*********************************************************

- z    ==> support  .gz extention or method
- j    ==> support  .bz2 extention or method
- J    ==> Support  .xz extention or method
*********************************************************


















