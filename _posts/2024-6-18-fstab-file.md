---
layout: post
title: fstab file Use
---

Whenever user do mounting with partition after reboot this is going to lapse to overcom this we generally do entery in the /etc/fstab file.
It is used to permanently mount filesystems.

**UUID Concept**

In fstab we can configure Universally Unique Identifiers (UUIDs) in the fstab file to identify file systems.
This ensures that disks can be automatically and correctly mounted even if the sequence in which the disks are attached is changed.

- Either we can enter partition name or UUID both are valid.

- blkid  - to get UUID of partitions


**Different fields and parameters in fstab file**

- 1. device name or partition name - usually given anem ro UUID of the mounted device.
- 2. Mount poing - any directory name.
- 3. File system type -  eg. ext2  ext3   ext4  xfs and more.
- 4. Options - lists any active mount options and if we use multiple separate them with commas normally we use default that includes like- read, write, suid, exec etc.
- 5. Backup - (the first digit) this is a binary system where 1=dump utility backup of a partition 0=no backup, this is the method and nowadays this is not in use.
- 6. file system check order - (Second digit) there are 3 outcome is possible - 0 means that fsck will not check the filesystem,
higher no. represent check order. The root file system should be 1  and normal partitions 2.


After doing entry in fstab file update the daemon by running below command-
- systemctl daemon-reload