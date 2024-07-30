---
 layout: post
 title: Key-value-array
---

   - 

   #!/bin/bash

   declare -A array

   array=( [name]=manoj [age]=29 [profile]="Devops Engineer" [salary]=45000)
   echo " name is : ${array[name]}, age is : ${array[age]}, profile is : ${array[profile]} and salary is : $ {array[salary]}"


