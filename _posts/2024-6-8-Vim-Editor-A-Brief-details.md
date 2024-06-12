---
layout: post
title: Vim Editor Brief Intro
---

Examples of File Controlling with Short keys
       OR
VIM advance Operation Notes with required Short keys in daily usages

=====================================================================

Types of mode in  vim editor ?

1- Insert Mode     ==>   to insert text into any file.

2- ESC Mode        ==>   to  perform any types of operation using any short keys

Example:  copy, paste, undo, redo, delete ...etc..

3- Command or  Colon Mode--->  to run any command.

Example:         :wq   (save and quit) 

====================================================

Vi and  Vim advance operation :-

# cp  /etc/passwd /root

# ls


# vim passwd  

Example of insert mode 

 i             { to insert text before the cursor }           ==> DONE    
 a             { to insert text after the cursor  }           ==> DONE 
 o             { to insert new line below of the cursor }     ==> DONE
 shit + o      { to insert line above of the cursor }         ==> DONE
      

Example of ESC  mode  ==>

 yy           { to copy any line } or  2yy ==> number of lines      ==> DONE
 p            { to paste the content }                              ==> DONE
 dd           { to delete any line }  or 2dd  or 5dd                ==> DONE
 u            { undo }                                              ==> DONE
 ctrl + r     { redo }                                              ==> DONE
 cc           { to cut copy any line } or 2cc                       ==> DONE
 yw	         { to copy any word }                               ==> DONE                         
 dw           { to delete any word }                                ==> DONE
 cw           { to cut copy word }                                  ==> DONE
 p            { to paste the content}                               ==> DONE
 shift + d    { to delete line from the cursor }                    ==> DONE
 x 	         { to delete particular characters in forward side } or 5x ==> DONE
 shift + x    { to delete particular characters in backward side }         ==> DONE
 shift + g    { to go in bottom of the file }
 gg	         { to move cursor in top of the file }
 zero            { to move cursor in begining of the line }{numeric zero } OR HOME
 shift + $       { to move cursor in end of the line } OR END


                k   UP
                -
                -
                -
  Left  h <-----------> l  right
                -
                -
                -
                j  DOWN



 b	         { to move cursor word by word in back side }   
 w	         { to move cursor word by word in forward side }
 /root	         { to search any pattern } 
                 { press n to jump on next pattern }
                 { press shift + n to jump on back pattern } 


Example of command or colon mode 

 :set number
  
   OR          { to set line number }

 :se nu

 :10        { to move cursor directly on any particular line number }
 :se nonu     { to remove line number }
 :se ic       { to deactivate the case-sensitive mode }
 /ROOT        { now it will work }
 :se noic     { to again activate the case-sensitive mode }
 :nohl	      { to remove highlight colors }
 :wq          { save and quit from any file }
      OR
 :x           { to save and quit from any file }  OR shift + zz  [example of ESC mode ]
 :q!          { to quit forcefully without save }
