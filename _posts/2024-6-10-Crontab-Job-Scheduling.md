---
layout: post
title: Schedule your tasks
---


**Crontab OR Job Scheduling**


* * * * * CMD


The * means all the possible unit — i.e every minute of every hour through out the year. 
More than using this * directly, 
you will find it very useful in the following cases. When you specify */5 in minute field 
means every 5 minutes. When you specify 0-10/2 
in minute field mean every 2 minutes in the first 10 minute. 
Thus the above convention can be used for all the other 4 fields.

----------------------------------------------------------------------------------------------------------

To schedule a job for more than one time (e.g. Twice a Day)
The following script take a incremental backup twice a day every day. This example executes the specified 
incremental backup shell script (incremental-backup) at 11:00 and 16:00 on every day. The comma separated 
value in a field specifies that the command needs to be executed in all the mentioned time.

00 11, 16 * * * /home/maverick/bin/incremental-backup


00 – 0th Minute (Top of the hour) 11, 16 – 11 AM and 4 PM * – Every day * – Every month * – Every day of the week


------------------------------------------------------------------------------------------------------------

6. To schedule a job for certain range of time (e.g. Only on Weekdays)
If you wanted a job to be scheduled for every hour with in a specific range of time then use the following.

Cron Job everyday during working hours : This example checks the status of the database everyday (including weekends) 
during the working hours 9 a.m – 6 p.m
00 09-18 * * * /home/maverick/bin/check-db-status


00 – 0th Minute (Top of the hour) 09-18 – 9 am, 10 am, 11 am, 12 am, 1 pm, 2 pm, 3 pm, 4 pm, 5 pm, 6 pm * – 
Every day * – Every month * – Every day of the week
Cron Job every weekday during working hours : This example checks the status of the database every weekday (i.e excluding Sat and Sun) 
during the working hours 9 a.m – 6 p.m.
00 09-18 * * 1-5 /home/maverick/bin/check-db-status


00 – 0th Minute (Top of the hour) 09-18 – 9 am, 10 am, 11 am, 12 am, 1 pm, 2 pm, 3 pm, 4 pm, 5 pm, 6 pm * – Every day * –
 Every month 1-5 -Mon, Tue, Wed, Thu and Fri (Every Weekday)
-----------------------------------------------------------------------------------------------------------

Cron special keywords and its meaning

Keyword    Equivalent
@yearly    0 0 1 1 *
@daily     0 0 * * *
@hourly    0 * * * *
@reboot    Run at startup.

---------------------------------------------------------------------------------------------------------




1- Crontab is use to schedule any task on any time.
2- with the help of crontab we can run any command
   and scripts on any time as per demand.

3- By default crontab service is allowed for super
   user and normal user  both.

4- Super user can set allow and deny rules for any normal users
   using   /etc/cron.deny and  /etc/cron.allow files.

Package:   crontabs 
Daemon name or  service name:   crond 
File:    /etc/crontab  
Log:   /var/log/cron  


*****************************************************************

# crontab   -l    { list ==> to check all crontab details in my account }

# crontab    -e   { edit ==> to apply crontab }

# crontab   -r    { Remove ==> to remove all cron jobs from my account }
 
******************************************************************

# crontab  -e   -u     username 

# crontab  -l   -u     username 

# crontab  -r   -u     username  

*******************************************************************

#  crontab  -e  

Here it will open  a file.. this file always devide  into two parts


First Field  ==>   Time Table   ==> break in five fields

First      second      Third     Fourth    Fifth 

Minutes    Hours    Day-of-Month   Month    days-of-week

(0 - 59)   (0-23)     (1-31)      (1-12)    (0 - 6 OR 1 - 7 ) [Where 0 and 7 => sunday]

Second Field ==>   Command to be executed  ==> again break in two Types of fiels

First Type   ==> we can run any particular command on defined time 
Second type  ==> we can any script file  on any defined yime


***********************************************************************
                       Possible Examples
***********************************************************************
30	09	*	*	*	      [ command - name or script - path ]
30	21	*	*	*	      [ command - name or script - path ]
30	09	*	*	1             [ command - name or script - path ]
30	09	*	*	1,3,5	      [ command - name or script - path ]
30	09	*	*	0,6	      [ command - name or script - path ]
30	09	*	*	1-5	      [ command - name or script - path ]
30	09	1,11,21	 *	*	      [ command - name or script - path ]
30	09	1       1,3,5	*	      [ command - name or script - path ]
30	09   1,3,5,11-15,21   * 	*     [ command - name or script - path ]
*/5	*	*	*	*	      [ command - name or script - path ]
*	*/2	*	*	*	      [ command - name or script - path ]
************************************************************************************

Value    ==> particular value
*        ==> all or every
,        ==> AND
-        ==> Range
/        ==> repeat