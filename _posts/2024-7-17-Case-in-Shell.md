---
 layout: post
 title: Case in Shell Scripting
--- 


**Case practice**

  
  #!/bin/bash

   echo "enter any choice"
   echo "Press a to print date"
   echo "Press b to print uptime"
   echo "Press c to check current location in system"

   read choice 

   case $choice in

	a)
		echo "Today date is :"
		date
		echo "Ending ......."
		;;

          


	b)
		echo "system uptime is :"
		uptime
		echo "Ending ......"
		;;

	c) echo "Current working directory is :"
		pwd
		echo "Ending ..........."
		;;

	*)echo "Please press valid keyword"
      esac

